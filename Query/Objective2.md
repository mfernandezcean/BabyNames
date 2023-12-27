#### Query for Births: 

```
SELECT Year, Gender, Name, SUM(Births) as num_babies
FROM names
GROUP BY 1,2,3;
```
### Rank the Names by Popularity (use previous query):

```
WITH babies_by_year AS (SELECT Year, Gender, Name, SUM(Births) as num_babies
FROM names
GROUP BY 1,2,3)

SELECT Year, Gender, Name, num_babies,
	row_number() over(Partition by Year, Gender Order by num_babies DESC) AS popularity  --- Creating a Ranking called 'popularity'
FROM babies_by_year;
```

|  Year	| Gender	 |Name	 | num_babies	|popularity |
|--|--|--|--|--|
|1980	  | F | Jennifer	|58.379	 |1 |
|1980	   | F| Amanda	|35.819	 |2 |
| 1980	  | F| Jessica	| 33.923	 |3|
| 1980	  | F| Melissa|31.634	| 4|
|... |... |... |... |... |
