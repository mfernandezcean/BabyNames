### Querying for the Top 10 most popular names for Girls:
```
SELECT name, SUM(Births) as Births_Sum 
FROM names
WHERE Gender = "F"
GROUP BY name
ORDER BY Births_Sum DESC
LIMIT 10;
```

| # name | Births_Sum |
|--|--|
|Jessica	  |  863.121|
|Ashley	|786.945
|Jennifer	 | 652.244|
| Sarah	| 621.174|
| Amanda	| 607.253|
|Emily	 |592.616 |
| Elizabeth	| 504.900|
| Samantha	| 479.347|
| Stephanie	| 417.748|
|Nicole	 |401.046 |

### Querying for the Top 10 most popular names for Boys:
```
SELECT name, SUM(Births) as Births_Sum 
FROM names
WHERE Gender = "M"
GROUP BY name
ORDER BY Births_Sum DESC
LIMIT 10;
```

| # name | Births_Sum |
|--|--|
|Michael	|  1.376.418|
|Christopher	|1.118.253
|Matthew	| 1.031.984|
| Joshua	| 957.518|
| Daniel	| 821.281|
|David	|816.976|
| James	| 764.296|
| Andrew	| 760.250|
| Joseph	| 754.667|
|John	|721.946|
---
### Querying for biggest Jump in popularity: 

#### Go to: [Window_Function](https://github.com/mfernandezcean/BabyNames/blob/main/Window_Function/Readme.md)

### Top 5 Increases:
| Year	 |Name	  | popularity1980	|Year	 |Name	 | popularity2009	|Increase of | 
|--|--|--|--|--|--|--|
|  1980	|  Colton	| 5789	|2009	 | Colton	| 149	|5640 |
| 1980	 | Aidan	 | 5691	| 2009	|Aidan	 | 109	|5582 |
| 1980	 | Rowan	 |5772	 |2009	 | Rowan	| 445	|5327 |
| 1980	 |Skylar	  | 5498	|2009	 |Skylar	 |313	 |5185 |
| 1980	 | Macy	 | 5615	|2009	 | Macy	| 571	|5044 |

### Top 5 Decreases:
| Year	 |Name	  | popularity1980	|Year	 |Name	 | popularity2009	|Decrease of | 
|--|--|--|--|--|--|--|
|  1980	|  Rusty	| 761	|2009	 | Rusty	| 9724	|8963|
| 1980	 | Tonia	| 879	| 2009	|Tonia	| 9548	|8669|
| 1980	 | Cherie	|808	|2009	 | Cherie	| 9347	|8539|
| 1980	 |Kerri	| 444	|2009	 |Kerri	|313	 |8279|
| 1980	 | Tarah		 | 1661	|2009	 | Tarah	| 9812	|8151|
