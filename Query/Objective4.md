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
