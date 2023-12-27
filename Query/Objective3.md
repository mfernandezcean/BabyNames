## Regions

```
SELECT distinct Region 
FROM regions;
```


| Region |  
|--|
| South | 
| Pacific|
| Mountain|
|New_England |
| Mid_Atlantic|
| Midwest|
| New England|

New England is repeated

```
SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions;
```

Checking:

```
WITH new_region AS(SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions)

SELECT DISTINCT new_region FROM new_region;
```

| Region |  
|--|
| South | 
| Pacific|
| Mountain|
|New_England |
| Mid_Atlantic|
| Midwest|

---

### Hint: MI is not represented in Midwest

```
WITH new_region AS(SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions)

SELECT DISTINCT n.State, nr.new_region
FROM names n LEFT JOIN new_region nr
	ON n.State = nr.State
WHERE new_region IS NULL ;
```

| State |new_region  |
|--|--|
| MI |null  |

Michigan does not have a region. We need to update to Midwest region.

```
WITH new_region AS(SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions
UNION					--- Use Union to stack both tables 
SELECT 'MI' AS State, 'Midwest' AS Region)

SELECT DISTINCT n.State, nr.new_region
FROM names n LEFT JOIN new_region nr
	ON n.State = nr.State;
```
### Good to go
---

#### Births by Region:

```
WITH new_region AS(SELECT State,
	   Case WHEN region = 'New England' Then 'New_England' ELSE Region END AS new_region
FROM regions
UNION
SELECT 'MI' AS State, 'Midwest' AS Region)

SELECT new_region, SUM(Births) as num_babies
FROM names n LEFT JOIN new_region nr
	ON n.State = nr.State
GROUP BY new_region;
```

|  new_region	| num_babies |
|--|--|
| Mid_Atlantic	 |13.742.667  |
| Midwest	 | 22.676.130 |
| Mountain	 | 6.282.217 |
| New_England	 | 4.269.213 |
| Pacific	 |  17.540.716|
| South	 | 34.219.920 |

--- 
### Most popular name by Region:
```
SELECT * FROM  		---> We subquery the rest so the Where < popularity enters in consideration
	(WITH babies_by_region AS (
		WITH new_region AS(SELECT State,
			   Case WHEN region = 'New England' Then 'New_England' ELSE Region END AS new_region
		FROM regions
		UNION
		SELECT 'MI' AS State, 'Midwest' AS Region)

		SELECT nr.new_region, n.Gender, n.Name, SUM(n.Births) as num_babies 
		FROM names n LEFT JOIN new_region nr
			ON n.State = nr.State
		GROUP BY 1,2,3)

	SELECT new_region, Gender, Name,
		row_number() OVER(partition by new_region, gender ORDER BY num_babies DESC) AS popularity ---> Popularity Ranking
	FROM babies_by_region) as x
WHERE popularity < 4;
```

###  Mid_Atlantic:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|Mid_Atlantic	 | F | Jessica	| 1|
| Mid_Atlantic	 | F |Ashley	 |2 |
| Mid_Atlantic	 | F |Jennifer	 | 3|
| Mid_Atlantic	 | M | Michael	| 1|
| Mid_Atlantic	 | M | Matthew	|2 |
| Mid_Atlantic	 | M |Christopher	 |3 |

### Midwest:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|Midwest	| F | Jessica	| 1|
| Midwest	| F |Ashley	 |2 |
| Midwest	| F |Sarah	| 3|
| Midwest	| M | Michael	| 1|
| Midwest	| M | Matthew	|2 |
| Midwest	| M |Joshua	|3 |

### Mountain:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|Mountain	| F | Jessica	| 1|
| Mountain	| F |Ashley	 |2 |
| Mountain	| F |Sarah	| 3|
| Mountain	| M | Michael	| 1|
| Mountain	| M | Joshua	|2 |
| Mountain	| M |Christopher	|3 |

### New_England:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|New_England	| F | Jessica	| 1|
| New_England	| F |Sarah	|2 |
| New_England	| F |Emily	| 3|
| New_England	| M | Michael	| 1|
| New_England	| M | Matthew	|2 |
| New_England		| M |Christopher	|3 |

### Pacific:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|Pacific	| F | Jessica	| 1|
| Pacific	| F |Jennifer	|2 |
| Pacific	| F |Ashley	| 3|
| Pacific	| M | Michael	| 1|
| Pacific	| M | Christopher	|2 |
| Pacific	| M |Daniel	|3 |

### South:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|South	| F | Ashley	| 1|
| South	| F |Jessica	|2 |
| South	| F |Jennifer	| 3|
| South	| M | Christopher	| 1|
| South	| M | Michael	|2 |
| South	| M |Joshua	|3 |
