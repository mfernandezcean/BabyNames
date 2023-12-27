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
---
### Querying for the Top 10 most popular names for Boys:
```
SELECT name, SUM(Births) as Births_Sum 
FROM names
WHERE Gender = "M"
GROUP BY name
ORDER BY Births_Sum DESC
LIMIT 10;
```
