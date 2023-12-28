### 10 Most popular Androgynous names:

```
SELECT * FROM(
	SELECT Name, COUNT(DISTINCT Gender) AS num_genders, SUM(Births) num_babies
	FROM names
	GROUP BY Name
	ORDER BY num_babies DESC
	LIMIT 10) x
WHERE num_genders > 1
;
```
| Name	 | num_genders	 |num_babies |
|--|--|--|
|  Michael	| 2 | 1.382.856
| Christopher	 |  2| 1.122.213
| Matthew	 | 2 | 1.034.494
|  Joshua	|  2| 960.170
| Jessica	 |  2| 865.046
| Daniel	 |  2| 824.208
|  David	|  2| 819.479
| Ashley	 |  2| 792.865
|  James	|  2| 766.789
| Andrew	 |  2| 761.824

---

### Shortest and Longest Names:

```
SELECT Name, LENGTH(Name) as name_length
FROM names
ORDER BY name_length ASC;

```
|Name	  | name_length |
|--|--|
| Ab	 | 2 |
| Ai	 | 2 |
| Aj	 | 2 |
| ... | ... |
| Yo	 | 2 |
| Yu	 | 2 |
| Zi	 | 2 |**

```
SELECT Name, LENGTH(Name) as name_length
FROM names
ORDER BY name_length DESC;
```
| Name	 | name_length |
|--|--|
| Franciscojavier	 | 15 |
| Johnchristopher	 | 15 |
|  Mariadelosangel	|  15|
|  Ryanchristopher	| 15 |

```
WITH short_long_names AS (Select *
FROM names
WHERE LENGTH(Name) IN (2,15))

SELECT Name, SUM(Births) AS num_babies
FROM short_long_names
GROUP BY Name
ORDER BY num_babies DESC;
```

|  Name	| num_babies |
|--|--|
| Ty	 |  29.205|
| Bo	 |  4.737|
| Jo	 | 1.713 |
| ... | ... |
| Su | 5 |
| Ta |5  |

---

### State withe the Highest % of Chrise's:

```
SELECT State, SUM(Births) AS num_chris
FROM names
WHERE name = 'Chris'
GROUP BY State;
```
Then:
```
With count_chris AS (Select State, SUM(Births) AS num_chris
FROM names
WHERE name = 'Chris' 	--> Only babies named Chris
GROUP BY State),


count_all AS (SELECT State, SUM(Births) AS num_babies
FROM names
GROUP BY State) 	--> all babies. 100%

SELECT *
FROM count_chris cc INNER JOIN count_all ca
	ON cc.State = ca.State;
```
To finish:
```
SELECT State, num_chris / num_babies * 100 AS pct_chris 
FROM  
(With count_chris AS (Select State, SUM(Births) AS num_chris
FROM names
WHERE name = 'Chris'
GROUP BY State),


count_all AS (SELECT State, SUM(Births) AS num_babies
FROM names
GROUP BY State)

SELECT cc.State, cc.num_chris, ca.num_babies
FROM count_chris cc INNER JOIN count_all ca
	ON cc.State = ca.State) AS state_chris_all
ORDER BY pct_chris DESC;
```

| State	 | % of Chris|
|--|--|
|LA	  | 0.0335 |
| HI	 | 0.0301 |
| NY	 | 0.0296 |
