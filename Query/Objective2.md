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

### Only the Top 3 names of Girls & Boys are of interest:

```
SELECT * FROM
	(WITH babies_by_year AS (SELECT Year, Gender, Name, SUM(Births) as num_babies
	FROM names
	GROUP BY 1,2,3)

	SELECT Year, Gender, Name, num_babies,
		row_number() over(Partition by Year, Gender Order by num_babies DESC) AS popularity
	FROM babies_by_year) x
Where popularity <=3;

```
Top 3 Girls:

 Year	 | Gender |Name |num_babies	 |popularity |
|--|--|--|--|--|
| 1980 |F  |Jennifer | 58.379	|1 |
|  1980| F | Amanda| 35.819|2 |
|  1980| F | Jessica|33.923 |3 |
| 1981 |  F|Jennifer |57.406 |1 |
|  1981| F | Jessica|42.530 | 2|
|1981  |F  |Amanda |34.372 | 3|
| ... |...  |... |... |... |
| 2008 | F |Emma	 |18.806	 |1 |
| 2008  | F |Isabella	 | 18.609	| 2|
| 2008  |  F| Emily	|17.426	 |3 |
| 2009 | F |Isabella	 |22.289	 |1 |
| 2009 |  F| Emma	| 17.889	| 2|
| 2009 | F |Olivia	 |17.429	 |3 |

Top 3 Boys:

| Year	 | Gender |Name |num_babies	 |popularity |
|--|--|--|--|--|
| 1980 |M  |Michael| 68.680|1 |
|  1980| M | Christopher| 49.091|2 |
|  1980| M | Jason|48.170 |3 |
| 1981 |  M|Michael|68.765 |1 |
|  1981| M | Christopher|50.228 | 2|
|1981  |M  |Matthew|43.324 | 3|
| ... |...  |... |... |... |
| 2008 | M |Jacob|22.587	 |1 |
| 2008  | M |Michael	 | 20.609	| 2|
| 2008  |  M| Ethan	|20.206	 |3 |
| 2009 | M |Jacob	 |21.162	 |1 |
| 2009 |  M| Ethan	| 19.839	| 2|
| 2009 | M |Michael	 |18.927	 |3 |
