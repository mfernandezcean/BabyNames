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

#### Midwest:
| new_region	 | Gender	 |Name	 | popularity |
|--|--|--|--|
|Mid_Atlantic	 | F | Jessica	| 1|
| Mid_Atlantic	 | F |Ashley	 |2 |
| Mid_Atlantic	 | F |Jennifer	 | 3|
| Mid_Atlantic	 | M | Michael	| 1|
| Mid_Atlantic	 | M | Matthew	|2 |
| Mid_Atlantic	 | M |Christopher	 |3 |
