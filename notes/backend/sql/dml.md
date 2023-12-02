# DML - Data Manipulation Language

## SELECT
```sql
    SELECT 
        column1, column2, ...
    FROM 
        table_name;
    JOIN 
        table_name ON condition
    WHERE 
        conditions
    GROUP BY 
        column_name
    HAVING 
        aggregate_function(column_name) operator value
    ORDER BY 
        column_name ASC/DESC
    LIMIT 
        first_value [, last_value]
```

## INSERT

> Вносит изменения в структуру таблиц: 
> добавляет запись (строки) и заполняет их значениями

```sql
    INSERT INTO table_name (column_name, ...) 
    VALUES (expressions, ...)
    RETURNING (column_name, ...) or *
```


## UPDATE

> Используется для изменения значений в записях таблицы

```sql
    UPDATE table_name 
    SET expression [WHERE condition]
    WHERE condition
    RETURNING (column_name, ...) or *
```

## DELETE

> Удаляет строки из временных или постоянных базовых таблиц

```sql
    DELETE FROM table_name 
    WHERE condition
```