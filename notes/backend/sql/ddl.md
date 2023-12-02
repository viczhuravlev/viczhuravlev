# DDL - Data Definition Language

## CREATE

> Создает данные

```sql
    CREATE TABLE  table_name (
        column_name1 data_type(size),
        column_name2 data_type(size),
        column_name3 data_type(size)
        ...
    )
```

## ALTER

> Вносить изменения в структуру уже существующей таблицы

```sql
    ALTER TABLE table_name
    ADD column_name data_type
```
* `ADD COLUMN column_name data_type` - добавляет новый столбец 
* `RENAME TO new_table_name` - переименовать таблицу
* `RENAME old_column_name TO new_column_name` - переименовать столбец
* `ALTER COLUMN column_name SET DATA TYPE data_type` - новый тип данных для солбца

## DROP

> Удаляет все

```sql
    DROP [ INDEX | TABLE | DATABASE | COLUMN ] object
```

## TRANCATE

> Удаляет все данные в таблице, если там нет ссылок на другие таблицы.

```sql
    TRUNCATE TABLE table_name
```