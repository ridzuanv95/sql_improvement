
# SQL improvement logic test
Based on the question given, a few improvement can be done to make query much more faster : 
- Create partial or multicolumn indexes for each table.

``` sql
Example : 

CREATE INDEX career_path_index ON CareerPaths(type, id, deleted);
```
- 
