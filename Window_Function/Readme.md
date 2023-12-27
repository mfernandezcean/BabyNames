## Window Function: 
### To create a popularity RANKING for Girls: 
```
SELECT Year, Name,
	row_number() over(partition by Year order by num_babies DESC) as popularity
FROM girl_names;
```
The return is the popularity for every Year:
|  # Year| Name	 | popularity|
|--|--|--|
|1980	  |  Jennifer	| 1|
| 1980	 | Amanda	 |2 |
| 1980	 |  Jessica	| 3|
| 1980	 | Melissa	 |4 |
| 1980	 |Sarah	  |5 |

![CTE popularity Girls](https://github.com/mfernandezcean/BabyNames/assets/105746149/6c1ee764-51bf-4e5b-99b7-6e6c0595853d)

We want to Know how the name 'Jessica' moved in popularity over the years:

```
SELECT Year, Name,
	row_number() over(partition by Year order by num_babies DESC) as popularity
FROM girl_names) x 
WHERE Name = "Jessica";
```
|# Year  |Name	  | popularity|
|--|--|--|
| 1980	 | Jessica	 |3 |
| 1981	 | Jessica	  | 2|
| 1982 | Jessica	  | 2|
| 1983 | Jessica	  | 2|
| 1984 |Jessica	   | 2|
| 1985 |Jessica	   |1 |
|  1986| Jessica	  | 1|
|  1987| Jessica	  | 1|
|  1988| Jessica	  |1 |
|  1989| Jessica	  | 1|
| 1990 | Jessica	  | 1|
|  1991| Jessica	  | 2|
| 1992 |Jessica	   |2 |
| 1993 | Jessica	  | 1|
|  1994| Jessica	  | 1|
|1995  | Jessica	  | 1|
|  1996|Jessica	   |2 |
| 1997 |  Jessica	 | 2|
|  1998| Jessica	  | 8|
| 1999 | Jessica	  |9 |
| 2000 | Jessica	  |8 |
| 2001 |Jessica	   |11 |
|  2002| Jessica	  | 16|
| 2003 | Jessica	  | 18|
| 2004 | Jessica	  | 21|
| 2005 | Jessica	  | 27|
| 2006 |  Jessica	 | 32|
| 2007 | Jessica	  |42|
|2008  | Jessica	  | 60|
|2009 |Jessica	   |78 |


![jessica and ashley chart](https://github.com/mfernandezcean/BabyNames/assets/105746149/7e80389c-6539-4e2c-8f16-3bdff68e93da)

### To create a popularity RANKING for Boys: 
```
SELECT name, SUM(Births) as Births_Sum 
FROM names
WHERE Gender = "M"
GROUP BY name
ORDER BY Births_Sum DESC
LIMIT 10;
```
| # name |Births_Sum  |
|--|--|
| Michael	 | 1.376.418 |
| Christopher	 | 1.118.253 |
| Matthew	 |  1.031.984|
|  Joshua	|  957.518|
| Daniel	|  821.281|
| David	| 816.976|
|  James	| 764.296|
| Andrew	 | 760.250 |
| Joseph	 |  754.667|
| John	 | 721.946 |

We want to Know how the name 'Michael' moved in popularity over the years:
|# Year  |Name	  | popularity|
|--|--|--|
| 1980	 | Michael|1 |
| 1981	 | Michael| 1|
| 1982 | Michael| 1|
| 1983 | Michael| 1|
| 1984 |Michael| 1|
| 1985 |Michael|1 |
|  1986| Michael| 1|
|  1987| Michael| 1|
|  1988| Michael|1 |
|  1989| Michael| 1|
| 1990 | Michael| 1|
|  1991| Michael| 1|
| 1992 |Michael|1|
| 1993 | Michael| 1|
|  1994| Michael| 1|
|1995  | Michael| 1|
|  1996|Michael|1|
| 1997 |  Michael| 1|
|  1998| Michael| 1|
| 1999 | Michael|2 |
| 2000 | Michael|2|
| 2001 |Michael|2 |
|  2002| Michael| 2|
| 2003 | Michael| 2|
| 2004 | Michael| 2|
| 2005 | Michael| 2|
| 2006 |  Michael| 2|
| 2007 | Michael|2|
|2008  | Michael| 2|
|2009 |Michael|3|

![michael and Cristopher chart](https://github.com/mfernandezcean/BabyNames/assets/105746149/06e5d67b-e0c5-49a5-8fb6-c56250f16577)

---
### JUMPS in Popularity:

```

WITH names_1980 AS(
	WITH all_names AS (SELECT Year, Name, SUM(births) AS num_babies
	FROM names
	GROUP BY Year, Name) 

	SELECT Year, Name,
		row_number() Over (Partition By Year Order By num_babies DESC) AS popularity1980
	FROM all_names
	WHERE Year = 1980), 							--Querying for popularity in 1980
    
names_2009 AS(
	WITH all_names AS (SELECT Year, Name, SUM(births) AS num_babies
	FROM names
	GROUP BY Year, Name)

	SELECT Year, Name,
		row_number() Over (Partition By Year Order By num_babies DESC) AS popularity2009
	FROM all_names
	WHERE Year = 2009) 							--Querying for popularity in 2009
    
SELECT * 
FROM names_1980 t1 INNER JOIN  names_2009 t2 ON t1.Name = t2.Name 		-- Joining 1980 and 2009
;
```
Behavior of Top 10 names in 1980:
| Year	 |Name	  | popularity1980	| Year	|Name	 |popularity2009 |
|--|--|--|--|--|--|
|1980	  |Michael	  | 1| 2009	|Michael	 |5 |
| 1980	   | Jennifer	 |2 |2009 |Jennifer	  |248 |
| 1980	   |  Christopher	| 3| 2009|Christopher	 | 14|
| 1980	   | Jason	 | 4| 2009|Jason | 96|
|1980	    | David	 |5 | 2009|David	  | 19|
|1980	    | James	 | 6|2009 | James	 |26 |
| 1980	   |  Matthew	| 7| 2009|Matthew	 |17 |
| 1980	   | Joshua	 |8 |2009 |Joshua	  |9 |
| 1980	   | Amanda	 |9 |2009 |Amanda	  | 363|
| 1980	   |  John | 10| 2009| John | 35|

## Check for Popularity Jumps between 2009 and 1980:

### Top 5 Increases

```
SELECT t1.Year, t1.Name, t1.popularity1980, t2.Year, t2.Name, t2.popularity2009,
	CAST(t2.popularity2009 AS SIGNED) - CAST(t1.popularity1980 AS SIGNED) AS _2009_diff_1980      --Cast to convert into numbers that can host negative values
FROM names_1980 t1 INNER JOIN  names_2009 t2 ON t1.Name = t2.Name 
ORDER BY _2009_diff_1980 ASC;
```
| Year	 |Name	  | popularity1980	|Year	 |Name	 | popularity2009	|Increase of | 
|--|--|--|--|--|--|--|
|  1980	|  Colton	| 5789	|2009	 | Colton	| 149	|5640 |
| 1980	 | Aidan	 | 5691	| 2009	|Aidan	 | 109	|5582 |
| 1980	 | Rowan	 |5772	 |2009	 | Rowan	| 445	|5327 |
| 1980	 |Skylar	  | 5498	|2009	 |Skylar	 |313	 |5185 |
| 1980	 | Macy	 | 5615	|2009	 | Macy	| 571	|5044 |

### Top 5 Decreases

```
SELECT t1.Year, t1.Name, t1.popularity1980, t2.Year, t2.Name, t2.popularity2009,
	CAST(t2.popularity2009 AS SIGNED) - CAST(t1.popularity1980 AS SIGNED) AS _2009_diff_1980  	--Cast to convert into numbers that can host negative values
FROM names_1980 t1 INNER JOIN  names_2009 t2 ON t1.Name = t2.Name 
ORDER BY _2009_diff_1980 DESC;
```
| Year	 |Name	  | popularity1980	|Year	 |Name	 | popularity2009	|Decrease of | 
|--|--|--|--|--|--|--|
|  1980	|  Rusty	| 761	|2009	 | Rusty	| 9724	|8963|
| 1980	 | Tonia	| 879	| 2009	|Tonia	| 9548	|8669|
| 1980	 | Cherie	|808	|2009	 | Cherie	| 9347	|8539|
| 1980	 |Kerri	| 444	|2009	 |Kerri	|313	 |8279|
| 1980	 | Tarah		 | 1661	|2009	 | Tarah	| 9812	|8151|
