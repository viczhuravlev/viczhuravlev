# Indexes

> Индекс - это структура данных, ускоряющая выборку данных из таблицы за счёт доп. операций записи и пространства на диске, используемых для хранения структуры данных и поддержания её в актуальном состоянии.

* Индекс - объект БД, который можно создать и удалить
* Позволяет искать значения без полного перебора
* Оптимизация выборки «небольшого» числа записей
  * «Небольшое» число - число относительное кол-ва записей
* По PRIMARY KEY и UNIQUE столбцам индекс создаётся автоматически
* Индексы не бесплатны

## Syntax

```sql
    CREATE INDEX index_name ON table_name (column _name))
```

Пример с задачей типа:

```sql
    CREATE INDEX index_name ON table_name USING HASH (column _name))
```

## Types

Покажет какие доступны в твоей БД
```sql
    SELECT amname FROM pg_am;
```

* B-tree (default) - сбалансированное дерево
  * Поддерживает операции: <, >, <=, >=, =
  * Поддерживает LIKE 'abc%' (но не '%abc')
  * Индексирует NULL
  * Сложность поиска O(log N)
* Hash - хеш-индекс
  * Поддреживате только оерацию "="
  * Не отражается в журнале предзаписи (WAL)
  * Не рекомендацется к применению (в общем и целом)
  * Сложность поиска O(1)
* GiST - обобщённое дерево поиска
  * Для индексации геометрических и текстовых данных
* GIN - обобщённый обратный
  * Для индексации массива или набора значений
* SP-GiST - GiST с двоичным разбиением пространства
  * Используется для естественной упорядоченности 
* BRIN - блочно-диапазонный
  * Используется на огромном количесвте данных с естественной упорядоченностью 

## Методы сканирования

* Index scan - индексное
* Index only scan - исключительно индексное сканирование
* Bitmap scan - сканирование по битовой карте
* Sequential scan - последовательное сканирование

