# SQL

## DDL - Data Definition Language

* CREATE
* ALTER
* DROP


## DML - Data Manipulation Language

### SELECT
```sql
    SELECT column1, column2, ...
    FROM table_name;
    WHERE condition
    GROUP BY column_name
    HAVING aggregate_function(column_name) operator value
    ORDER BY column_name ASC/DESC
    LIMIT first_value [, last_value]
```

### INSERT

### UPDATE

### DELETE

## Math

* `+` - сложение
* `-` - вычитание 
* `*` - умножение 
* `/` - деление 
* `^` - степень 
* `|/` - квадратный корень
* ect...

## Functions

### COUNT - функция возвращающая количество записей (строк) таблицы.
```sql
    SELECT COUNT(*)
    FROM table_name
```

### MIN - функция возвращающая минимальное значение столбца
```sql
    SELECT MIN(column_name)
    FROM table_name
```

### MAX - ункция возвращающая максимальное значение столбца таблицы
```sql
    SELECT MAX(column_name)
    FROM table_name
```

### AVG - функция возвращающая среднее значение столбца
```sql
    SELECT AVG(column_name)
    FROM table_name
```

### SUM — функция, возвращающая сумму значений столбца таблицы
```sql
    SELECT SUM(column_name)
    FROM table_name
```


## Operators

### DISTINCT - только уникальне значения столбца
```sql
    SELECT DISTINCT column_name 
    FROM table_name
```

### BETWEEN - задает диапазон, в котором будет осуществляться проверка условия
```sql
    SELECT *
    FROM table_name
    WHERE column_name BETWEEN 100 AND 300
```

### IN - позволяет определить, совпадает ли значение объекта со значением в списке
| Используется вместо перечисления через OR оператор
```sql
    SELECT *
    FROM table_name
    WHERE column_name IN ('UK', 'USA')
```

### NOT - служит для задания противоположно заданного условия
```sql
    SELECT *
    FROM table_name
    WHERE column_name NOT IN ('UK', 'USA')
```

### LIKE - устанавливает соответствие символьной строки с шаблоном

Pattern matching:

`%` - placeholder означающий 0,1 и более символов

`_` - ровно 1 любой символ

* `LIKE 'U%'` - строки, начинающиеся с U
* `LIKE '%a'` - строки, кончающиеся на а
* `LIKE '%John%'` - строки, содержащие John
* `LIKE 'J%n'` - строки, начинающиеся на J, и кончающиеся на п
* `LIKE '_oh_'` - строки, где 2, 3 символы - oh, а первый (1) и последний (4) - любые
* `LIKE '_oh%'` - строки, где 2, 3 символы - oh, первый - любой и в конце 0, 1 и более любых символов

```sql
    SELECT *
    FROM table_name
    WHERE column_name NOT IN ('UK', 'USA')
```

### UNION / UNION ALL - объединения двух и более запросов
![Union](./images/sql/union.png)
```sql
    SELECT column_name(s) FROM table1
    UNION
    SELECT column_name(s) FROM table2
```

### INTERSECT - выбирает пересечения двух и более запросов
![Intersect](./images/sql/intersect.png)
```sql
    SELECT column_name(s) FROM table1
    INTERSECT
    SELECT column_name(s) FROM table2
```

### MINUS / EXCEPT - вернет все строки с первого SELECT, которые не вернулись вторым SELECT
![Except](./images/sql/except.png)
```sql
    SELECT column_name(s) FROM table1
    EXCEPT
    SELECT column_name(s) FROM table2
```