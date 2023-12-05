# Triggers

> Объект, который назначает действие на те или иные события. Триггеры могут реагировать как на построчное изменение (множественное срабатывание), так и единожды на все изменения сразу

Для чего используют триггеры:
* Аудит таблиц
* Дополнительные действия в ответ на изменения
* Сложные проверки целостности

Что необходимо, что бы тригеры работали:
* Для совершения действия необходима функция
* И сам объект триггера

## "Построчные" триггеры

```sql
    -- Создание триггера:
    CREATE TRIGGER trigger_name() condition ON table_name
    FOR EACH ROW EXECUTE PROCEDURE function_name();
    
    -- Condition:
    [BEFORE, AFTER] [INSERT, UPDATE, DELETE]
    
    -- Например:
    BEFORE INSERT
    AFTER UPDATE
    BEFORE INSERT OR UPDATE
    
    --Удаление: 
    DROP TRIGGER IF EXISTS trigger_name
```

## Функции на пострачные триггеры

```sql
    CREATE FUNCTION func_name () RETURNS trigger AS $$
        BEGIN
        ----
        END;
    §$ LANGUAGE plpgsal;
```

* Должна возвращать NULL или запись, соответствующую структуре таблицы, на которую будет вешаться триггер!
* Через аргумент NEW есть доступ к вставленным и модифицированным строкам
(INSERT/UPDATE триггеры)
* Через аргумент OLD есть доступ к вставленным и удалённым строкам
(UPDATE/DELETE триггеры)

## Управление объектами триггеров

```sql
    -- Создание триггера
    CREATE TRIGGER trigger_name() condition ON table_name
    REFERENCING [NEW, OLD] TABLE AS ref_table_name
    FOR EACH STATEMENT EXECUTE PROCEDURE function_name();

    -- Удаление триггера:
    DROP TRIGGER IF EXISTS trigger_ name ON table_ name
    
    -- Переименование триггера:
    ALTER TRIGGER trigger name ON table name
    RENAME TO new_trigger_name;
    
    -- Отключение триггера:
    ALTER TABLE table name
    DISABLE TRIGGER trigger_name;
    
    -- Отключение всех триггеров на таблице:
    ALTER TABLE table name
    DISABLE TRIGGER ALL;
```

## Советы по возврату из триггеров

* Должна возвращать NULL или запись, соответствующую структуре таблицы, на которую будет вешаться триггер!
* Если BEFORE-триггер возвращает NULL, то сама операция и AFTER-триггеры будут отменены
* BEFORE-триггер может изменить строку (INSERT\UPDATE) через NEW и тогда операция и AFTER-триггеры будут работать с изменённой строкой
* Если BEFORE-триггер не «хочет» изменять строку, то надо просто вернуть NEW
* В случае BEFORE-триггера реагирующего на DELETE, возврат не имеет значения (кроме NULL: отменит DELETE)
* NEW = null при DELETE, так что если BEFORE-триггер хочет дать ход DELETE, надо вернуть OLD
* Возвращаемое значение из построчного AFTER-триггера (или и из BEFORE и из AFTER триггеров на утверждения) игнорируется => можно возвращать NULL
* Если построчный AFTER-триггер или триггер на утверждение хочет отменить операцию => raise exception


## Пример

```sql
    -- function
    CREATE OR REPLACE FUNCTION track_changes() RETURNS TRIGGER AS $$
    begin
        new.last_update = now();
        return new;
    end
    $$ LANGUAGE PLPGSQL;

    -- using
    CREATE TRIGGER column_timestamp 
    BEFORE INSERT OR UPDATE ON table_name
    FOR EACH ROW EXECUTE PROCEDURE track_changes();
```