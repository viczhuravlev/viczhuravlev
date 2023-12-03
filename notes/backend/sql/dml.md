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

## CASE WHEN

> Позволяет писать условия в выборке 

```sql
    CASE
        WHEN condition_1 THEN result_1
        WHEN condition_2 THEN result_2
        [WHEN ...]
        [ELSE result_n]
    END
```

Пример:

```sql
    SELECT column_name1, column_name2,
        CASE
            WHEN date_part('month', column_date) BETWEEN 3 AND 5 THEN 'spring'
            WHEN date_part('month', column_date) BETWEEN 6 AND 8 THEN 'summer'
            WHEN date_part('month', column_date) BETWEEN 9 AND 11 THEN 'autumn'
            ELSE 'winter'
        END AS season
    FROM orders;
```


