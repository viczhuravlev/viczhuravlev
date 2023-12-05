# Security

## Уровни безопасности

* Экземпляра (кластера/сервера/инсталляции): аутентификация, создание БД, управление безопасностью и т.д.
* Базы данных: подключение к конкретной БД, создание в ней ролей и т.д.
* Схемы: управление схемами (создание, удаление)
* Таблицы: CRUD-операции над таблицами
* Колонки: операции над конкретной колонкой конкретной таблицы
* Строки таблицы

## Privilege

```sql
    -- Создать роль с привелегиями
    CREATE ROLE role_name [PRIVILEGE];

    -- Посмотреть список ролей
    SELECT rolname FROM pg_roles

    -- Создать роль с пользователем
    CREATE ROLE role_name LOGIN;
    CREATE USER user_name;
    CREATE USER user_name WITH PASSWORD '******';
    CREATE ROLE role_name -- создает бесправную роль (NOLOGIN, NOSUPERUSER и т.д.)

```

По умолчанию выдает все права с `NO`.

* LOGIN [NOLOGIN] - позволяет логинеться
* SUPERUSER [NOSUPERUSER] - обходит все пермишены, кроме логина. Лучше не работать из под этой роли
* CREATEDB [NOCREATEDB] - позволяет создавать.
* CREATEROLE [NOCREATEROLE] - позволяет создавать, удалять или изменять роли. Если «user» имеет привилегию CREATEROLE, но не CREATEDB, то он может создать новую роль с правами CREATEDB! CREATEROLE - почти SUPERUSER!
* REPLICATION [NOREPLICATION] - дает доступ к репликациям(создания копий).

## Удалить роль

Чтобы удалить роль, необходимо:
* изъять все выданные ранее права
* переназначить все объекты на другую роль, которыми владела удаляемая роль

```sql
    -- Передать все жругой роли 
    ALTER TABLE table name OWNER TO other role
    
    -- Удалить все незначимые объекты, которыми владела удаляемая роль
    DROP OWNED BY deleting_role [CASCADE] [RESTRICT], restrict is default

    -- Изъять все права с таблиц
    REVOKE ALL PRIVILEGES ON table1, table2... FROM deleting_role
    
    -- Снять доступ к базе данных
    REVOKE ALL ON DATABASE db name FROM deleting role
    
    -- Снять доступ со схемы
    REVOLE ALL ON SCHEMA schema name FROM deleting role
    
    -- Удаляем пользователя
    DROP ROLE [IF EXISTS] deleting_role

```


## Доступ к таблице

```sql
    GRANT operation ON TABLE table name TO role
```

Operation:
* SELECT
* INSERT
* UPDATE
* DELETE
* TRUNCATE
* REFERENCES - создание внешних ключей

## Доступ к колонкам

```sql
    GRANT operation (columns) ON TABLE table_name TO role
```

Operation:
* SELECT
* INSERT
* UPDATE
* REFERENCES - возможность ссылаться на колонки с внешним ключом

## Доступ к строкам

> После включения row-level security, доступ к данным запрещён

> Две и более политик работают как запросы с UNION между ними, т.е. в результирующий набор будут включаться все данные из этих политик, даже если они по смыслу друг другу противоречат

```sql
    ALTER TABLE table ENABLE ROW LEVEL SECURITY;
    
    -- Если необходимо дать доступ явно через политику:
    CREATE POLICY policy_name ON table_name
    FOR operation TO role
    USING (expression)

    -- Удалить
    DROP POLICY policy_name ON table_name
```
