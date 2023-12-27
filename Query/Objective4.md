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
