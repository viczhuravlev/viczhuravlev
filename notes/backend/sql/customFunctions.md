# Custom functions

## Типы

* SQL-функции
* Процедурные (PL/pgSQL - основной диалект)
* Серверные функции (написанные на С)
* Собственные С-функции

## Syntax

```sql
    CREATE OR REPLACE FUNCTION func_name(larg1, arg2...]) 
    RETURNS data_type AS $$
    --logic
    S$ LANGUAGE lang
```

Example simple function:

```sql
    CREATE OR REPLACE FUNCTION get_total_number() RETURNS bigint AS $$
	    SELECT SUM(column_number) AS total_number 
        FROM table_name
    $$ LANGUAGE SQL;


    SELECT get_total_number() AS total_number;
```

Example with params:

```sql
    CREATE OR REPLACE FUNCTION get_price_(count int DEFAULT 1, OUT max_price real, OUT min_price real) AS $$
        SELECT MAX(column_price), MIN(column_price)
        FROM table_name
        WHERE column_count = count
    $$ LANGUAGE SQL;
```

## Возврат множества строк

* `RETURNS SETOF data type` - возврат п-значений типа data type
* `RETURNS SETOF table` - если нужно вернуть все столбцы из таблицы или пользовательского типа
* `RETURNS SETOF record` - только когда типы колонок в результирующем наборе заранее неизвестны
* `RETURNS TABLE (column_name data_type, ...)` - тоже что и setof table, но имеем возможность явно указать возвращаемые столбцы
* Возврат через `out`-параметры


## PL / pgSQL

```sql
    CREATE FUNCTION func_name([arg1, arg2...]) RETURNS data_ type AS $$
        DECLARE
            variable type;
        BEGIN
            --logic
        END;
    S$ LANGUAGE plpgsal;
```


### If / else

```sql
    IF expression THEN 
        logic
    ELSIF expression THEN
        logic
    ELSIF expression THEN
        logic
    ELSE
        logic
    END IF;
```

### Loop

```sql
    WHILE expression
    LOOP 
        logic
    END LOOP;
```

```sql
    LOOP
        EXIT WHEN expression 
        logic
    END LOOP;
```

```sql
    FOR counter IN a..b [BY ×]
    LOOP 
        logic
    END LOOP;
```

```sql
    CONTINUE WHEN expression
```