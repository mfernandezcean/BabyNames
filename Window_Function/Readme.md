### Window Function: 
To create a popularity RANKING: 
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
