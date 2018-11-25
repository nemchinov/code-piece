> PostgreSQL — это реляционная система управления базами данных (представленными в виде отношений (relation)). Отношение — это математически точное обозначение таблицы. 
Любая таблица представляет собой именованный набор строк. Все строки таблицы имеют одинаковый набор именованных столбцов, при этом каждому столбцу назначается определённый тип данных. Хотя порядок столбцов во всех строках фиксирован, важно помнить, что SQL не гарантирует какой-либо порядок строк в таблице (хотя их можно явно отсортировать при выводе).
1. `psql -U username -h localhost -p 5432 dbname`
1. `psql -l` - db list
1.  Таблицы
    ```sql
    CREATE TABLE cities (
        city varchar(80) primary key,
        location point NOT NULL
    );

    CREATE TABLE weather (
        city varchar(80) references cities(city),
        temp int DEFAULT 9
    );
    ```
    Наследование - не интегрировано с ограничениями уникальности и внешними ключами
    ```sql
    CREATE TABLE capitals (
        state char(2)
    ) INHERITS (cities);
    -- запрос FROM cities выведет данные из обеих таблиц,
    -- для получения данных из конкретной таблицы -  FROM only cities
    DROP TABLE IF EXISTS capitals;
    ```
    Ограничения  
    * `price numeric CHECK (price > 0)`, `CONSTRAINT positive_price CHECK (price > 0)` - имя  positive_price будет выводиться в ошибках  
        можно задавать отдельной строкой `..., CHECK (discounted_price > 0 AND price > discounted_price), ...`
    * `NOT NULL` / `NULL`
    * `UNIQUE`, `UNIQUE (a, c)` - для группы столбцов
    * `PRIMARY KEY`, `PRIMARY KEY(a, c)` - уникальный не равный NULL, автоматически создаётся уникальный индекс-B-дерево
    * Внешние ключи - `REFERENCES table (field)`
1. Представления
    ```sql
    CREATE VIEW myview AS
        SELECT city, temp FROM weather, cities
        WHERE city = name;
    ```
1. Транзакции
    ```sql
    BEGIN;
    UPDATE accounts SET balance = balance - 100.00
        WHERE name = 'Alice';
    COMMIT;
    -- SAVEPOINT my_savepoint; ROLLBACK TO my_savepoint;
    ```
1. Оконные функции
    ```
    имя_функции ([выражение [, выражение ... ]]) [ FILTER ( WHERE предложение_фильтра ) ] OVER ( определение_окна )
    -- определение окна
    [ имя_существующего_окна ]
    [ PARTITION BY выражение [, ...] ]
    [ ORDER BY выражение [ ASC | DESC | USING оператор ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ определение_рамки ]
    ```
    ```sql
    SELECT depname, empno, salary, rank() OVER w
    FROM empsalary
    WINDOW w AS (PARTITION BY depname ORDER BY salary DESC);
    SELECT salary, sum(salary) OVER () FROM empsalary; -- сумма всех строк
    SELECT salary, sum(salary) OVER (ORDER BY salary) FROM empsalary; -- суммирование по строчно в порядке сортировки
    ```
1. Массивы
    ```sql
    SELECT (ARRAY[1,2,4] || 5)[2:4];
    SELECT ARRAY[]::integer[];--создание пустого массива
    ```
1. Агрегирующие функции
    ```
    агрегатная_функция ( [ выражение [ , ... ] ] ) WITHIN GROUP ( предложение_order_by ) [ FILTER ( WHERE условие_фильтра ) ]
    ```
1. Предложение COLLATE переопределяет правило сортировки выражения
1. Row Constructors - выражение, создающее строку или кортеж  
    ```sql
    SELECT ROW(1,2.5,'this is a test');
    SELECT (1,2.5,'this is a test');
    SELECT ROW(t.*, 42) FROM t;
    ```  
1. Права 
    ```sql
    GRANT UPDATE ON accounts TO joe;
    REVOKE ALL ON accounts FROM PUBLIC;
    ```
1. Returning `INSERT INTO users Default VALUES RETURNING id;`

# Info
1. Максимальная длинна имени идентификатора - NAMEDATALEN равно 64 - 1байт
1. Экранирование 
    - апостроф `''`
    - спецсимволы `\\, \n, \', ...`
    - Игнорирование 
        ```sql
        $$Жанна д'Арк$$
        $SomeTag$Жанна д'Арк$SomeTag$
        ```
1. Операторы
    - `!` - факториал
1. Большинство агрегатных функций игнорируют значения NULL
1. Массивы 
    - Многомерные массивы должны быть прямоугольными
    - Массив не может быть не типизированным
    - Индексация с единицы
1. Число столбцов в таблице ограничивается максимумом в пределах от 250 до 1600, в зависимости от типов столбцов. 
1. В секционированных таблицах первичные ключи не поддерживаются, на секционированные таблицы не могут ссылаться внешние ключи. 
1. Сторонние данные - FOREIGN DATA - обращение к данным, находящимся снаружи, используя обычные SQL-запросы.