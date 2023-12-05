# Views

> Результат выполнения запроса к базе данных, определенного с помощью оператора SELECT, в момент обращения к представлению.

## Types

* Временные
* Рекурсивные
* Обновляемые
* Материализуемые

## Syntax

```sql
    CREATE VIEW view_name AS
    SELECT select_statment
```

OR 

```sql
    CREATE OR REPLACE VIEW view_name AS
    SELECT select_statment
```

## Rename

```sql
    ALTER VIEW old_view_name RENAME 
    TO new_view_name
```

## Remove

```sql
    DROP VIEW [IF EXISTS] view_name
```
