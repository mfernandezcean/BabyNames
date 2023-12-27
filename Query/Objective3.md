## Regions

```
SELECT distinct Region 
FROM regions;
```


| Region |  
|--|
| South | 
| Pacific|
| Mountain|
|New_England |
| Mid_Atlantic|
| Midwest|
| New England|

New England is repeated

```
SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions;
```

Checking:

```
WITH new_region AS(SELECT State,
	   Case WHEN region = ' New England' Then 'New_England' ELSE Region END AS new_region
FROM regions)

SELECT DISTINCT new_region FROM new_region;
```

| Region |  
|--|
| South | 
| Pacific|
| Mountain|
|New_England |
| Mid_Atlantic|
| Midwest|
