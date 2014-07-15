###### 查询重复数据
```sql
SELECT * FROM table1
WHERE field IN (
    SELECT field FROM table2 GROUP BY field HAVING count(field) > 1
) 
```

###### 连接字符串
```sql
SELECT concat('_',hello,'_') FROM table WHERE field='test'
```

###### 查表定义
```sql
DESCRIBE chatlogs_pop
``` 
