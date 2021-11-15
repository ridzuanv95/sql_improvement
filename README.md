
# SQL Query Improvement Test
Based on the question given, a few improvement can be done to make query much more faster : 
1. Implementing partial or multicolumn indexes for each column that we used to search and filter on each table.

``` sql
Example : 

CREATE INDEX career_path_index ON CareerPaths(type, id, deleted);
```

2. For `WHERE` method based on this part :
``` sql
WHERE ((JobCategories.name LIKE '%キャビンアテンダント%'
OR JobTypes.name LIKE '%キャビンアテンダント%'
OR Jobs.name LIKE '%キャビンアテンダント%'
OR Jobs.description LIKE '%キャビンアテンダント%'
OR Jobs.detail LIKE '%キャビンアテンダント%'
OR Jobs.business_skill LIKE '%キャビンアテンダント%'
OR Jobs.knowledge LIKE '%キャビンアテンダント%'
OR Jobs.location LIKE '%キャビンアテンダント%'
OR Jobs.activity LIKE '%キャビンアテンダント%'
OR Jobs.salary_statistic_group LIKE '%キャビンアテンダント%'
OR Jobs.salary_range_remarks LIKE '%キャビンアテンダント%'
OR Jobs.restriction LIKE '%キャビンアテンダント%'
OR Jobs.remarks LIKE '%キャビンアテンダント%'
OR Personalities.name LIKE '%キャビンアテンダント%'
OR PracticalSkills.name LIKE '%キャビンアテンダント%'
OR BasicAbilities.name LIKE '%キャビンアテンダント%'
OR Tools.name LIKE '%キャビンアテンダント%'
OR CareerPaths.name LIKE '%キャビンアテンダント%'
OR RecQualifications.name LIKE '%キャビンアテンダント%'
OR ReqQualifications.name LIKE '%キャビンアテンダント%')
AND publish_status = 1
AND (Jobs.deleted) IS NULL)
```
Improvement that can be made is by removing wildcard in `LIKE` and use `IN` or `=` since querying exact value is faster than comparing using `LIKE`. For example :
``` sql
Change Jobs.name LIKE '%キャビンアテンダント%'
To Jobs.name = 'キャビンアテンダント' / Jobs.name IN 'キャビンアテンダント'
```

3. Creating temporary tables based on which table that will be used for search query since query used a lot of `JOIN` multiple table. For example : 
``` sql
SELECT id, name, job_category_id, sort_order, created_by, created, modified, deleted
INTO #JobTypesPriority
FROM job_types
WHERE name = 'キャビンアテンダント'
```
Temporary tables are very useful when database have a large number of records in a table and query need to repeatedly interact with a small subset of those records. In such cases instead of filtering the data again and again to fetch the subset, you can filter the data once and store it in a temporary table. You can then execute your queries on that temporary table.

## Time Taken
Time taken to complete this is around 2 days.
