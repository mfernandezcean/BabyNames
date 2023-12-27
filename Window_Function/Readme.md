### Window Function: 
To create a popularity RANKING: 
```
SELECT Year, Name,
	row_number() over(partition by Year order by num_babies DESC) as popularity
FROM girl_names;
```
