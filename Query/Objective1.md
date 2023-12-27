
```
SELECT n.*,
max(births) over(partition by year) as max_births
FROM names n ;
```

