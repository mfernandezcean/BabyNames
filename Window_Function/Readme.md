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
