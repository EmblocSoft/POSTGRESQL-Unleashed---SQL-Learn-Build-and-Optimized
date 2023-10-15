
POSTGRESQL 16 Unleashed - SQL Learn, Build, and Optimize
</br></br>
Welcome! 

A. 
The Book is published on Amazon </br>

[https://www.amazon.com/SQL-Certification-Expert-Insights-Practice-ebook/dp/B0CJG5DZ52/ref=sr_1_50?crid=1DFJZY2ZP98Q7&keywords=SQL&qid=1695604933&sprefix=s%2Caps%2C300&sr=8-50](https://www.amazon.com/dp/B0CL2JND72/ref=sr_1_8?keywords=postgresql+16&qid=1697330833&sr=8-8)

</br>

B. SQL up and running: </br>

For a seamless installation experience, visit the GitHub repository at 
https://github.com/EmblocSoft/PostgreSQL 
and download the graphical installer program. This easy-to-use tool will equip you with everything you need to dive into the world of SQL and 
start building your database skills in no time!

</br>

C. Practices
</br>

p1.1 & p1.2
</br>
-- To create a new database</br>

CREATE DATABASE my_db; 
</br></br>

p1.3
</br>

CREATE TABLE t1 (i INT, d1 DOUBLE PRECISION , d2 DOUBLE PRECISION);

</br>

INSERT INTO t1 VALUES 
(1, 101.40, 31.40), 
(1, -70.00, 0.00),
(2, 0.00, 0.00), 
(2, -13.20, 0.00), 
(2, 59.60, 46.40),
(2, 30.40, 30.40), 
(3, 37.00, 7.40), 
(3, -29.60, 0.00),
(4, 60.00, 15.40), 
(4, -10.60, 0.00), 
(4, -34.00, 0.00),
(5, 33.00, 0.00), 
(5, -25.80, 0.00), 
(5, 0.00, 7.20),
(6, 0.00, 0.00), 
(6, -51.40, 0.00);

</br>

SELECT i, SUM(d1) AS a, SUM(d2) AS b
FROM t1 
GROUP BY i 
HAVING SUM(d1) <> SUM(d2) 
ORDER BY i;

</br>

SELECT   i, SUM(d1) AS a, SUM(d2) AS b
FROM     t1 
GROUP BY i 
HAVING (ROUND(SUM(d1)::NUMERIC - SUM(d2)::NUMERIC)) <> 0 
ORDER BY i;

</br></br>


p2:</br>
CREATE TABLE t2 (
    my_int               INT, 
    my_smallint          SMALLINT,
    my_bigint            BIGINT,
    my_numeric           NUMERIC,
    my_real              REAL,
    my_double            DOUBLE PRECISION, 
    my_smallserial       SMALLSERIAL,
    my_serial            SERIAL,
    my_bigserial         BIGSERIAL,
    my_money             MONEY,
    my_char_varying      CHARACTER VARYING(20),
    my_varchar           VARCHAR(20),
    my_char              CHAR(20),
    my_text              TEXT,
    my_bytea             BYTEA,
    my_timestamp_0       TIMESTAMP(0) WITHOUT TIME ZONE,
    my_timestamp_3       TIMESTAMP(3) WITHOUT TIME ZONE,
    my_timestamp_6       TIMESTAMP(6) WITHOUT TIME ZONE,
    my_timestamp_tz_0    TIMESTAMP(0) WITH TIME ZONE,
    my_timestamp_tz_3    TIMESTAMP(3) WITH TIME ZONE,
    my_timestamp_tz_6    TIMESTAMP(6) WITH TIME ZONE,
    my_date              DATE,
    my_time              TIME(6),
    my_time_tz           TIME(6) WITH TIME ZONE,
    my_interval_0        INTERVAL MINUTE TO SECOND (0),
    my_interval_3        INTERVAL MINUTE TO SECOND (3),
    my_interval_6        INTERVAL MINUTE TO SECOND (6),
    my_boolean           BOOLEAN,
    my_xml               XML,
    my_json              JSON,
    my_jsonb             JSONB,
    my_char_array        CHAR[],
    my_text_array        TEXT[],
    my_uuid              UUID,
    my_inet              INET,
    my_cidr              CIDR,
    my_macaddr           MACADDR,
    my_macaddr8          MACADDR8,
    my_tsvector          TSVECTOR);

</br></br></br>

p2.1</br>
INSERT INTO t2 ( my_int,  my_real, my_double)
VALUES (1, 1.12345678901234567890, 1.123456789012345678901234567890);
</br></br>
SELECT my_int, my_real, my_double, my_serial FROM t2 WHERE my_int = 1;

</br></br></br>

p2.2</br>
INSERT INTO t2 (my_int, my_numeric)
VALUES (2, 12345678901234567890.12345678901234567890);

SELECT my_int, my_numeric, my_smallserial, my_bigserial FROM t2 WHERE my_int = 2;
</br></br></br>


p2.3</br>
INSERT INTO t2 (my_int, my_numeric) VALUES (3, 'Infinity');
INSERT INTO t2 (my_int, my_numeric) VALUES (4, '-Infinity');
INSERT INTO t2 (my_int, my_numeric) VALUES (5, 'NaN');
</br>
SELECT my_int, my_numeric FROM t2;
SELECT 'Infinity'::NUMERIC /  'Infinity'::NUMERIC AS t;
SELECT 'Infinity'::NUMERIC /  '-Infinity'::NUMERIC AS t;

</br></br></br>

p2.4</br>
INSERT INTO t2 (my_int, my_money)
VALUES (6, 12345678.912345678901234567890);
</br>
SELECT my_int, my_money, my_serial FROM t2 WHERE my_int = 6;
SELECT CURRVAL(pg_get_serial_sequence('t2', 'my_serial'));

</br></br></br>

p2.5</br>
SELECT my_int, my_money / 5 AS amount FROM t2 WHERE my_int = 6;
SELECT my_int, my_money / 1.5 as amount FROM t2 WHERE my_int = 6;
SELECT my_int, (my_money::NUMERIC / 1.5)::MONEY as amount FROM t2 WHERE my_int = 6;

</br></br></br>

p2.6</br>
INSERT INTO t2 (my_int, my_char_varying, my_varchar, my_char, my_text)
VALUES (
7, 'abcdefghijklmnopqrst', 'abcdefghijklmnopqrst', 
'abcdefghijklmnopqrstu', 'abcdefghijklmnopqrstuvwxyz');
</br>
SELECT my_char_varying, my_varchar, my_char, my_text FROM t2 WHERE my_int =7;

</br></br></br>

p2.7</br>
INSERT INTO t2 (my_int, my_char_varying, my_varchar, my_char, my_text)
VALUES (8, 'abcdefghijklmnopqrst', 'abcdefghijklmnopqrst', 
'abcdefghijklmnopqrstu', 'abcdefghijklmnopqrstuvwxyz');
</br></br>
SELECT my_char_varying, my_varchar, my_char, my_text FROM t2 WHERE my_int = 8;
</br></br>
INSERT INTO t2 (my_int, my_char_varying, my_varchar, my_char, my_text)
VALUES (9, 'abcdefghijklmnopqrstu', 'abcdefghijklmnopqrstu', 'abcdefghijklmnopqrstu', 'abcdefghijklmnopqrstuvwxyz');
(This will return ERROR)
</br></br>
INSERT INTO t2 (my_int, my_char_varying, my_varchar, my_char, my_text)
VALUES (
9, 'abcdefghijklmnopqrstuvwxyz'::VARCHAR(20), ' abcdefghijklmnopqrstuvwxyz '::VARCHAR(20), 
' abcdefghijklmnopqrstuvwxyz '::CHAR(20), 'abcdefghijklmnopqrstuvwxyz');
</br></br>
SELECT my_char_varying, my_varchar, my_char, my_text FROM t2 WHERE my_int = 9;

</br></br></br>

p2.8</br>
INSERT INTO t2 (my_int, my_bytea)
VALUES (10, E'\\xDEADBEEF');
</br></br>
SELECT my_int, my_bytea FROM t2 WHERE my_int = 10;
</br></br>
SET bytea_output = 'hex';
SELECT my_int, my_bytea FROM t2 WHERE my_int = 10; -- same SELECT statement
</br></br>
SET bytea_output = 'escape';
SELECT my_int, my_bytea FROM t2 WHERE my_int = 10;  -- same SELECT statement


</br></br></br>
p2.9</br>
INSERT INTO t2 (
    my_int,
    my_timestamp_0,         --TIMESTAMP(0) 
    my_timestamp_3,         --TIMESTAMP(3)
    my_timestamp_6,         --TIMESTAMP(6)
    my_timestamp_tz_0,      --TIMESTAMP(0) WITH TIME ZONE
    my_timestamp_tz_3,      --TIMESTAMP(3) WITH TIME ZONE
    my_timestamp_tz_6,      --TIMESTAMP(6) WITH TIME ZONE
    my_date,
    my_time,                --TIME(6)
    my_time_tz              --TIME(6) WITH TIME ZONE
)
VALUES (
    11,
    TIMESTAMP '2023-08-03 12:34:56',
    TIMESTAMP '2023-08-03 12:34:56.789',
    TIMESTAMP '2023-08-03 12:34:56.123456',
    TIMESTAMPTZ '2023-08-03 12:34:56+00:00',
    TIMESTAMPTZ '2023-08-03 12:34:56.789+00:00',
    TIMESTAMPTZ '2023-08-03 12:34:56.123456+00:00',
    DATE '2023-08-03',
    TIME '12:34:56',
    TIME '12:34:56+00:00'
);
</br></br>
\x on  
</br></br>
SELECT my_int, my_timestamp_0, my_timestamp_3,my_timestamp_6,
       my_timestamp_tz_0,my_timestamp_tz_3, my_timestamp_tz_6,
       my_date, my_time, my_time_tz
FROM   t2 
WHERE  my_int = 11;
</br></br></br>


p2.10</br>
INSERT INTO t2 (my_int, my_date, my_time, my_time_tz)
VALUES (
    12,
    'now'::DATE,
    'allballs'::TIME,
    'allballs'::TIME WITH TIME ZONE
);
</br></br>
SELECT my_int, my_date, my_time, my_time_tz FROM t2 WHERE my_int = 12;  
</br></br>
INSERT INTO t2 (
    my_int, 
    my_date,
    my_time,
    my_timestamp_tz_0
)
VALUES (
    13,
    'yesterday'::DATE,
    'now'::TIME,
    'now'::TIMESTAMP WITH TIME ZONE
);
</br></br>
SELECT my_int, my_date, my_time, my_timestamp_tz_0 FROM t2 WHERE my_int = 13;

</br></br></br>

p2.11</br>
INSERT INTO t2 (
    my_int,
    my_timestamp_0,         --TIMESTAMP(0) 
    my_timestamp_3,         --TIMESTAMP(3)
    my_timestamp_6,         --TIMESTAMP(6)
    my_timestamp_tz_0,      --TIMESTAMP(0) WITH TIME ZONE
    my_timestamp_tz_3,      --TIMESTAMP(3) WITH TIME ZONE
    my_timestamp_tz_6       --TIMESTAMP(6) WITH TIME ZONE
)
VALUES (
    14,
    TIMESTAMP '2023-12-31 23:59:59',
    TIMESTAMP '2024-01-01 00:00:00.000',
    TIMESTAMP '2025-01-01 00:00:00.000000',
    TIMESTAMPTZ '2023-12-31 23:59:59+08:00',
    TIMESTAMPTZ '2024-01-01 00:00:00.000+08:00',
    TIMESTAMPTZ '2025-01-01 00:00:00.000000+08:00'
);
 </br></br>
SELECT
     my_int,
     my_timestamp_3 - my_timestamp_0        AS t1_duration,
     my_timestamp_6 - my_timestamp_0        AS t2_duration,
     my_timestamp_tz_3 - my_timestamp_tz_0  AS t3_duration,
     my_timestamp_tz_6 - my_timestamp_tz_3  AS t4_duration
FROM t2
WHERE my_int = 14;
</br></br>
SELECT
    my_int,
    EXTRACT(EPOCH FROM (my_timestamp_3 - my_timestamp_0))         AS t1_duration,
    EXTRACT(EPOCH FROM (my_timestamp_6 - my_timestamp_0))         AS t2_duration,
    EXTRACT(EPOCH FROM (my_timestamp_6 - my_timestamp_3))         AS t3_duration,
    EXTRACT(EPOCH FROM (my_timestamp_tz_3 - my_timestamp_tz_0 ))  AS t4_duration,
    EXTRACT(EPOCH FROM (my_timestamp_tz_6 - my_timestamp_tz_0 ))  AS t5_duration,
    EXTRACT(EPOCH FROM (my_timestamp_tz_6 - my_timestamp_tz_3 ))  AS t6_duration
FROM t2
WHERE my_int = 14;

</br></br></br>

p2.12</br>
INSERT INTO t2 (
    my_int,
    my_timestamp_0,         --TIMESTAMP(0) 
    my_timestamp_3          --TIMESTAMP(3)
)
VALUES (
    15,
    TIMESTAMP '2023-12-31 23:59:59',
    TIMESTAMP '2023-12-31 23:59:59'  + 
     INTERVAL '2 Years 3 Months 17 Days 3 Hours 20 Minutes 8 Seconds'
);

</br></br></br>
SELECT
      my_int,
      my_timestamp_0,
      my_timestamp_3,
      my_timestamp_3 - my_timestamp_0        AS t1_duration
FROM  t2
WHERE my_int = 15;
</br></br>
SELECT TO_CHAR(INTERVAL '3 Hours 20 Minutes 8 Seconds', 'HH12:MI:SS') AS timing;
SELECT (INTERVAL '1 Year 2 Months 1 Day 3 Hours 20 Minutes 1 Second') AS timing;
</br></br>
SELECT EXTRACT(HOURS FROM INTERVAL '1 Year 2 Months 1 Day 3 Hours 20 Minutes 1 Second') 
AS timing;
</br></br>
CREATE TABLE event (
    event_name VARCHAR(100),
    event_duration INTERVAL(4)
);
</br></br>
INSERT INTO event (event_name, event_duration)
VALUES ('Meeting', INTERVAL '3 hours 30 minutes 15.1234 seconds');
</br></br>
SELECT * FROM event;
</br></br></br>


p2.13</br>
INSERT INTO t2 (
    my_int,
    my_varchar,         
    my_boolean          
)
VALUES (
    16,
    'Buy groceries', 
    TRUE
);
</br></br>
SELECT
      my_int,
      my_varchar,         
      my_boolean          
FROM  t2
WHERE my_int = 16;
</br></br>
SELECT 'yes'::BOOLEAN AS is_true, NULL::BOOLEAN AS is_false;

</br></br></br>

p2.14</br>
CREATE TYPE MOOD AS ENUM ('sad', 'ok', happy');
</br></br>
CREATE DOMAIN POSTAL_CODE AS TEXT
CHECK(VALUE ~ '^\d{5}$' OR VALUE ~ '^\d{5}-\d{4}$');

CREATE TABLE t3 (
   my_int          INT,
   my_mood         MOOD,
   my_postal_code  POSTAL_CODE);
</br></br>
INSERT INTO t3 (
    my_int,
    my_mood,         
    my_postal_code          
)
VALUES (
    1,
    'happy', 
    '01234-1234'
);
</br></br>
SELECT my_int, my_mood, my_postal_code FROM t3 WHERE my_int =1;

</br></br></br>

p2.15</br>
INSERT INTO t2 (my_int, my_json) --JSON
VALUES (
   17,
   '{"title": "DBA Guidebook", "author": "Moss", "published_year": 2023}'
);
</br></br>
SELECT 
   my_int, 
   my_json->>'title' AS title, 
   my_json->>'author' AS author, 
  (my_json->>'published_year')::INTEGER AS published_year
FROM t2 
WHERE my_int = 17;
</br></br>
INSERT INTO t2 (my_int, my_jsonb)  --JSONB
VALUES (
   18,
   '{"title": "DBA Guidebook", "author": "Moss", "published_year": 2023}'
);
</br></br>
SELECT 
   my_int, 
   my_jsonb->>'title' AS title, 
   my_jsonb->>'author' AS author, 
  (my_jsonb->>'published_year')::integer AS published_year
FROM t2 
WHERE my_int = 18;


</br></br></br>
p2.16</br>
SELECT 
   my_int, 
   my_json->>'title' AS title, 
   my_json->>'author' AS author, 
  (my_json->>'published_year')::integer AS published_year
FROM t2 
WHERE my_int = 17;
</br></br>
SELECT 
   my_int, 
   my_json->'title' AS title, 
   my_json->'author' AS author, 
  (my_json->'published_year') AS published_year
FROM t2 
WHERE my_int = 17;

</br></br></br>

p2.17</br>
SELECT
   my_int,
   my_json #> '{title}' AS title,
   my_json #> '{author}' AS author,
   my_json #> '{published_year}' AS published_year
FROM t2
WHERE my_int = 17;

</br></br></br>

p2.18</br>
SELECT '{"a":1, "b":2}'::jsonb @> '{"b":2}'::jsonb AS checked;
SELECT '{"b":2}'::jsonb <@ '{"a":1, "b":2}'::jsonb  AS checked;
SELECT '{"a":1, "b":2}'::jsonb ? 'b' AS checked;

</br></br></br>

p2.19</br>
INSERT INTO t2 (my_int, my_json)
VALUES (
    18,
    to_json('{"title": "SQL Certification"}'::json)
);
</br></br>
SELECT
   my_int,
   my_json #> '{title}' AS title
FROM t2
WHERE my_int = 18;
</br></br>
SELECT array_to_json('{{1,5},{99,100}}'::int[]) AS checked;
</br></br>

INSERT INTO t2 (my_int, my_jsonb)
VALUES (
    19,
    jsonb_build_object(
        'title', 'Data Visualization',
        'author', 'Antonia',
        'published_year', '2023'::jsonb
    )
);
</br></br>
SELECT
   my_int,
   my_jsonb #> '{title}' AS title,
   my_jsonb #> '{author}' AS author,
   my_jsonb #> '{published_year}' AS published_year
FROM t2
WHERE my_int = 19;
 </br></br>
SELECT 
   my_int, 
   my_jsonb->>'title' AS title, 
   my_jsonb->>'author' AS author, 
  (my_jsonb->>'published_year') AS published_year
FROM t2 
WHERE my_int = 19;
</br></br>

INSERT INTO t2 (my_int, my_jsonb)
VALUES (
    20,
    jsonb_build_array(
        '{"title": "SQL Certification"}'::jsonb,
        '{"author": "Moss"}'::jsonb,
        '{" published_year ": 2023}'::jsonb
    )
);
</br></br>
SELECT 
   my_int, my_jsonb
FROM t2 
WHERE my_int = 20;
</br></br>
SELECT 
   my_int, 
   my_jsonb->0->>'title'  AS title, 
   my_jsonb->1->>'author' AS author, 
  (my_jsonb->2->>'published_year ')::int AS published_year
FROM t2 
WHERE my_int = 20;

</br></br>
INSERT INTO t2 (my_int, my_jsonb)
VALUES (
    21,
    to_jsonb('{"title": "DBA Guidebook", "author": "Moss", "published_year": 2023}'::jsonb)
);
</br></br>
SELECT
   my_int,
   my_jsonb->>'title' AS title,
   my_jsonb->>'author' AS author,
   (my_jsonb->>'published_year')::int AS published_year
FROM t2
WHERE my_int = 21;

</br></br>
INSERT INTO t2 (my_int, my_jsonb)
VALUES (
  22,
  array_to_json(ARRAY[jsonb_build_object(
    'title', 'DBA Guidebook', 'author', 'Moss', 'published_year', 2023)
    ]
  )
);
</br></br>
SELECT
   my_int,
   (my_jsonb #> '{0,title}') AS title,
   (my_jsonb #> '{0,author}') AS author,
  ((my_jsonb #> '{0,published_year}')::int) AS published_year
FROM t2
WHERE my_int = 22;

</br></br>
INSERT INTO t2 (my_int, my_jsonb)
VALUES (
  23,
  row_to_json(
     (SELECT r FROM (SELECT 'DBA Guidebook' AS title, 'Moss' AS author, 2023 AS published_year) AS r)
    )
);
</br></br>
SELECT
   my_int,
   my_jsonb->>'title' AS title,
   my_jsonb->>'author' AS author,
   (my_jsonb->>'published_year')::int AS published_year
FROM t2
WHERE my_int = 23;

</br></br>
INSERT INTO t2 (my_int, my_jsonb)
VALUES (
    24,
    json_object(
        ARRAY['title', 'author', 'published_year'],
        ARRAY['DBA Guidebook', 'Moss', '2023']
    )::jsonb
);
</br></br>
SELECT
   my_int,
   my_jsonb->>'title' AS title,
   my_jsonb->>'author' AS author,
   (my_jsonb->>'published_year')::int AS published_year
FROM t2
WHERE my_int = 24;


</br></br></br>
p2.20</br>
SELECT my_int, jsonb_each(my_jsonb) FROM t2 WHERE my_int =24;

</br></br></br>

p2.21</br>
INSERT INTO t2 (my_int, my_xml)
VALUES (25, '<root><element>Example XML</element></root>');
</br></br>
SELECT my_int, my_xml from t2 where my_int=42;

</br></br></br>

p2.22</br></br>
CREATE TABLE t4 (
    my_int            INT,
    my_varchar_array  VARCHAR[],
    my_int_array      INT[3],
    my_numeric_array  NUMERIC[],
    my_boolean_array  BOOLEAN[],
    my_date_array     DATE[]
);
</br></br>
INSERT INTO t4 (my_int, my_varchar_array) VALUES (1, '{"value1", "value2", "value3"}');
</br></br>
INSERT INTO t4 (my_int, my_int_array) VALUES (2, '{1, 2, 3}');
</br></br>
INSERT INTO t4 (my_int, my_numeric_array) VALUES (3, '{1.23, 4.56, 7.89}');
</br></br>
INSERT INTO t4 (my_int, my_boolean_array) VALUES (4, '{true, false, true}');
</br></br>

INSERT INTO t4 (my_int, my_date_array)  
VALUES (5, '{"2023-05-01", "2023-05-15", "2023-06-01"}');
</br></br>
SELECT my_varchar_array[1] FROM t4 WHERE my_int = 1;
</br></br>
SELECT my_int_array[2] FROM t4 WHERE my_int = 2;
</br></br>
SELECT my_numeric_array[3] FROM t4 WHERE my_int = 3;
</br></br>
SELECT my_boolean_array[1] FROM t4 WHERE my_int = 4;
</br></br>
SELECT my_date_array[2]    FROM t4 WHERE my_int = 5;
</br></br></br>


p2.23</br>
CREATE TABLE t5 (
    my_int            INT,
    my_int4range      INT4RANGE,
    my_numrange       NUMRANGE,
    my_tsrange        TSRANGE,     --Timestamp range without time zone
    my_tstzrange      TSTZRANGE,   --Timestamp range with time zone
    my_varchar        VARCHAR,
    my_value          NUMERIC
);
</br></br>
INSERT INTO t5 (my_int, my_tsrange, my_varchar, my_value)
VALUES (1, '[2023-08-01 00:00:00, 2023-08-02 00:00:00)', 'USD/EUR', 1.221);
</br></br>
INSERT INTO t5 (my_int, my_tsrange, my_varchar, my_value)
VALUES (2, '[2023-08-02 00:00:00, 2023-08-03 00:00:00)', 'USD/EUR', 1.222);
</br></br>
INSERT INTO t5 (my_int, my_tsrange, my_varchar, my_value)
VALUES (3, '[2023-08-03 00:00:00, 2023-08-04 00:00:00)', 'USD/EUR', 1.223);
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE  my_tsrange  @> '2023-08-03'::TIMESTAMP;
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE my_tsrange  @> '2023-08-02'::TIMESTAMP;
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE my_tsrange  @> '2023-08-01'::TIMESTAMP;
</br></br>
INSERT INTO t5 (my_int, my_tstzrange, my_varchar, my_value)
VALUES (4, '[2023-08-01 00:00:00+8, 2023-08-02 00:00:00+8)', 'USD/EUR', 1.224);
</br></br>
INSERT INTO t5 (my_int, my_tstzrange, my_varchar, my_value)
VALUES (5, '[2023-08-02 00:00:00+8, 2023-08-03 00:00:00+8)', 'USD/EUR', 1.225);
</br></br>
INSERT INTO t5 (my_int, my_tstzrange, my_varchar, my_value)
VALUES (6, '[2023-08-03 00:00:00+8, 2023-08-04 00:00:00+8)', 'USD/EUR', 1.226);
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE my_tstzrange  @> '2023-08-01'::TIMESTAMP WITH TIME ZONE;
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE my_tstzrange  @> '2023-08-02'::TIMESTAMP WITH TIME ZONE;
</br></br>
SELECT my_varchar AS Currency, my_value AS rate FROM t5
WHERE my_tstzrange  @> '2023-08-03'::TIMESTAMP WITH TIME ZONE;

</br></br></br>

p2.24</br>
INSERT INTO t5 (my_int, my_int4range, my_varchar, my_value)
VALUES (11, '[0, 1)', 'New Born', 50000);
</br></br>
INSERT INTO t5 (my_int, my_int4range, my_varchar, my_value)
VALUES (12, '[1, 7)', 'Kid', 100000);
</br></br>
INSERT INTO t5 (my_int, my_int4range, my_varchar, my_value)
VALUES (13, '[7, 18)', 'Young', 150000);
</br></br>
INSERT INTO t5 (my_int, my_int4range, my_varchar, my_value)
VALUES (14, '[18, 60)', 'Adult', 200000);
</br></br>
INSERT INTO t5 (my_int, my_int4range, my_varchar, my_value)
VALUES (15, '[60, 150)', 'Old', 250000);
</br></br>
SELECT my_varchar, my_value FROM t5 WHERE my_int4range @> 18;
</br></br>
INSERT INTO t5 (my_int, my_numrange, my_varchar, my_value)
VALUES (21, '[0.00, 50.00)', 'Low Price Range', 0.05);
</br></br>
INSERT INTO t5 (my_int, my_numrange, my_varchar, my_value)
VALUES (22, '[50.00, 150.00)', 'Mid Price Range', 0.08);
</br></br>
INSERT INTO t5 (my_int, my_numrange, my_varchar, my_value)
VALUES (23, '[150.00, 1000]', 'High Price Range', 0.10);
</br></br>
SELECT my_varchar, my_numrange, my_value AS extra_discount FROM t5
WHERE my_numrange @> '50'::NUMERIC;
</br></br>
SELECT my_varchar, my_numrange, my_value AS extra_discount FROM t5
WHERE my_numrange @> '49.99999'::NUMERIC;
</br></br>
SELECT my_varchar, my_numrange, my_value AS extra_discount FROM t5
WHERE my_numrange @> '150.00'::NUMERIC;

</br></br></br>

p2.25</br>
INSERT INTO t2 (my_int, my_uuid, my_varchar)
VALUES (26, 'a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11', 'Data validation Job');
</br></br>
INSERT INTO t2 (my_int, my_inet, my_varchar)
VALUES (27, '192.168.0.1', 'Database server IP');
</br></br>
INSERT INTO t2 (my_int, my_cidr, my_varchar)
VALUES (28, '192.168.0.0/24', 'CIDR Range');
</br></br>
INSERT INTO t2 (my_int, my_macaddr, my_varchar)
VALUES (29, '08:00:2b:01:02:03', 'MAC Address');
</br></br>
INSERT INTO t2 (my_int, my_macaddr8, my_varchar)
VALUES (30, '08:00:2b:01:02:03:04:05', 'MAC Address 8'); 

</br></br></br>

p2.26</br>
INSERT INTO t2 (my_int, my_text, my_tsvector)
VALUES (
   31, 
   'Using dedicated data types for UUID, CIDR, INET, MACADDR, and MACADDR8 can lead to better data management', 
   to_tsvector('english', 'Using dedicated data types for UUID, CIDR, INET, MACADDR, and MACADDR8 can lead to better data management')
);
</br></br>
INSERT INTO t2 (my_int, my_text, my_tsvector)
VALUES (
   32, 
   'As database systems evolve, they can introduce optimizations and enhancements specific to these data types. Storing the data in dedicated columns will allow you to take advantage of such improvements without needing to change your data model.', 
   to_tsvector('english', 'As database systems evolve, they can introduce optimizations and enhancements specific to these data types. Storing the data in dedicated columns will allow you to take advantage of such improvements without needing to change your data model.')
);
</br></br>
INSERT INTO t2 (my_int, my_text, my_tsvector)
VALUES (
   33, 
   ' Storing MAC addresses alongside network configuration settings for various devices to ensure proper configuration and connectivity.', 
   to_tsvector('english', 'Storing MAC addresses alongside network configuration settings for various devices to ensure proper configuration and connectivity.'));
</br></br>
SELECT my_text, my_tsvector FROM t2 WHERE my_int =31;
</br></br>
SELECT my_int, my_text
FROM t2
WHERE my_tsvector @@ to_tsquery('english', 'data & types')
ORDER BY ts_rank_cd(my_tsvector, to_tsquery('english', 'better & data')) DESC;
</br></br>
SELECT my_int, my_text
FROM t2
WHERE my_tsvector @@ to_tsquery('english', 'data & types')
ORDER BY ts_rank_cd(my_tsvector, to_tsquery('english', ' improvements & enhancements')) DESC;
</br></br></br>


p3.</br>
CREATE DATABASE about_x;
</br></br>
\l
</br></br>
\c about_x
</br></br>
CREATE SCHEMA car;
</br></br>
CREATE SCHEMA space;
</br></br>
CREATE SCHEMA common;
</br></br>
\dn
</br></br></br>


p3.1</br>
-- Create the ENUM about allowed values of title
CREATE TYPE ENUM_TITLE AS ENUM ('Mr.', 'Ms.', 'Mrs.', 'Dr.', 'Prof.');
</br></br>
-- Create the Shareholder table under the common schema
CREATE TABLE common.shareholder (
    shareholder_id VARCHAR(10) PRIMARY KEY,
    title       ENUM_TITLE,
    first_name  VARCHAR(30) NOT NULL,
    middle_name VARCHAR(30),
    last_name   VARCHAR(30) NOT NULL,
    email       VARCHAR(30) NOT NULL,
    phone       VARCHAR(30) NOT NULL,
    address_1   VARCHAR(30) NOT NULL,
    address_2   VARCHAR(30),
    address_3   VARCHAR(30),
    address_4   VARCHAR(30),
    city        VARCHAR(30) NOT NULL,
    country     VARCHAR(30) NOT NULL,
    postal_code VARCHAR(8) NOT NULL
);
</br></br>
-- Create indexes
CREATE INDEX shareholder_idx_01 ON common.shareholder (shareholder_id);
CREATE INDEX shareholder_idx_02 ON common.shareholder (first_name, last_name, shareholder_id);
</br></br>
-- Insert sample data
INSERT INTO common.shareholder (
 shareholder_id, title, first_name, middle_name, last_name, email, phone,
 address_1, address_2, address_3, address_4,
 city, country, postal_code
)
VALUES(
 'S000000001',
 'Mr.', 'Elon', 'Reeve', 'Musk','Elon.musk@x.com', '+1-010101010101',
 'Unit 1 X Corp Building', NULL, NULL, NULL, 'Los Angeles', 'USA', '912345');

</br></br></br>

p3.2</br>
-- Create the Shareholder Registry table under the common schema
CREATE TABLE common.shareholder_registry (
    company        VARCHAR(50) NOT NULL,
    shareholder_id VARCHAR(10) NOT NULL,
    shares         BIGINT NOT NULL,
    PRIMARY KEY (shareholder_id, company),
    FOREIGN KEY (shareholder_id) REFERENCES common.shareholder (shareholder_id)
);
</br></br>
-- Create index
CREATE INDEX share_reg_idx_01 ON common.shareholder_registry (company, shareholder_id);
</br></br>
-- Insert sample data
INSERT INTO common.shareholder_registry (
 company, shareholder_id, shares)
VALUES ('xSpace Inc', 'S000000001', 100000000);
</br></br>
INSERT INTO common.shareholder_registry (
 company, shareholder_id, shares)
VALUES ('E Car Inc', 'S000000001', 200000000);
</br></br>
INSERT INTO common.shareholder_registry (
 company, shareholder_id, shares)
VALUES ('X Inc', 'S000000001', 300000000);
</br></br>
SELECT s.title, s.first_name, s.last_name, sr.shares
FROM common.shareholder s
JOIN common.shareholder_registry sr ON s.shareholder_id = sr.shareholder_id;
</br></br></br>


p3.3</br>
-- Create the xSpace Travel Schedule table under the space schema
CREATE TABLE space.space_travel_schedule (
    trip_id        VARCHAR(10) PRIMARY KEY,
    destination    VARCHAR(100) NOT NULL,
    departure_from VARCHAR(100) NOT NULL,
    departure_dtm  TIMESTAMP(0) NOT NULL,
    return_dtm     TIMESTAMP(0) NOT NULL,
    price          MONEY NOT NULL
);
</br></br>
-- Create indexes
CREATE INDEX space_idx_01 ON space.space_travel_schedule (trip_id);
</br></br>
CREATE INDEX space_idx_02 ON space.space_travel_schedule (destination, trip_id);
</br></br>
-- Insert sample data
INSERT INTO space.space_travel_schedule (
 trip_id, destination, departure_from,
 departure_dtm, return_dtm, price)
VALUES (
 'S000000001', 'Moon', 'Los Angeles, USA',
 '2024-12-31 23:59:59', '2025-01-31 00:00:00', 1000000.00);
</br></br></br>


p3.4</br>
-- Create the Customer table under the car schema
CREATE TABLE car.customer (	 
    customer_id VARCHAR(20) PRIMARY KEY,
    title       ENUM_TITLE,
    first_name  VARCHAR(30) NOT NULL,
    middle_name VARCHAR(30),
    last_name   VARCHAR(30) NOT NULL,
    email       VARCHAR(30),
    phone       VARCHAR(30),
    address_1   VARCHAR(30),
    address_2   VARCHAR(30),
    address_3   VARCHAR(30),
    address_4   VARCHAR(30),
    city        VARCHAR(30),
    country     VARCHAR(30),
    postal_code VARCHAR(8),
    tweeter_account_id VARCHAR(64)
);
</br></br>
-- Create index
CREATE INDEX customer_idx_01 ON car.customer (customer_id);
</br></br>
-- Insert sample data
INSERT INTO car.customer (
 customer_id, title, first_name, middle_name, last_name,
 email, phone,  
 address_1, address_2, address_3, address_4,
 city, country, postal_code, 
 tweeter_account_id)
VALUES (
 'C230000001', 'Mr.', 'Thomas', 'S', 'Bright',
 'thomas@thomassbright.org', '+01-123456789', 
 'Unit 1, First Street', NULL, NULL, NULL,
 'Los Angeles', 'USA', '923456',
 '@thomassbright');

</br></br></br>

p3.5</br>
-- Create the Space Trip table under the space schema
CREATE TABLE space.space_trip (
    trip_id     VARCHAR(10) PRIMARY KEY,
    customer_id VARCHAR(10) NOT NULL,
    fee         MONEY NOT NULL,
    amount_paid MONEY NOT NULL,
    FOREIGN KEY (customer_id) REFERENCES car.customer(customer_id)
);
</br></br>
-- Create indexes
CREATE INDEX trip_idx_01 ON space.space_trip (trip_id, customer_id);
</br></br>
CREATE INDEX trip_idx_02 ON space.space_trip (customer_id, trip_id);
</br></br>
-- Insert sample data
INSERT INTO space.space_trip (trip_id, customer_id, fee, amount_paid)
VALUES ('S000000001', 'C230000001', '1,000,000.00', '900,000.00');
</br></br>
SELECT st.trip_id, sch.destination, sch.departure_dtm,
       c.first_name, c.last_name, 
       st.amount_paid
FROM space.space_trip st
JOIN car.customer c ON st.customer_id = c.customer_id
JOIN space.space_travel_schedule sch ON st.trip_id = sch.trip_id;
</br></br></br>


p3.6</br>
-- Create the Product Category table under the car schema
CREATE TABLE car.category (
    category_id VARCHAR(20) PRIMARY KEY,
    description TEXT NOT NULL
);
</br></br>
-- Create the Product Category table under the car schema
CREATE TABLE car.category (
    category_id VARCHAR(20) PRIMARY KEY,
    description TEXT NOT NULL
);
</br></br>
-- Create index
CREATE INDEX category_idx_01 ON car.category (category_id);
</br></br>
-- Insert sample data
INSERT INTO car.category (category_id, description)
VALUES ('CT000001', 'Advanced model');

</br></br></br>

p3.7</br>
-- Create the Category Designer table under the car schema
CREATE TABLE car.category_designer (
    category_id VARCHAR(20) REFERENCES car.category (category_id),
    designer    VARCHAR(50) NOT NULL,
    PRIMARY KEY (category_id, designer)
);
</br></br>
-- PRIMARY KEY (category_id, designer):  specifies that the combination of the category_id and designer columns will be the primary key
CREATE INDEX category_designer_idx_01 ON car.category_designer (category_id, designer);
</br></br>
INSERT INTO car.category_designer (category_id, designer)
VALUES ('CT000001', 'Arthur');
</br></br>
INSERT INTO car.category_designer (category_id, designer)
VALUES ('CT000001', 'Antonia');

</br></br></br>

p3.8</br>
-- Create the Product table under the car schema
CREATE TABLE car.product (
    product_id   VARCHAR(20) PRIMARY KEY,
    product_name TEXT NOT NULL,
    sku          VARCHAR(20) NOT NULL,
    origin       VARCHAR(20) NOT NULL,
    color        VARCHAR(20) NOT NULL,
    category_id  VARCHAR(20) NOT NULL,
    price        MONEY NOT NULL,
    FOREIGN KEY (category_id) REFERENCES car.category(category_id)
);
</br></br>
-- Create indexes
CREATE INDEX product_idx_01 ON car.product (product_id);
CREATE INDEX product_idx_02 ON car.product (category_id, product_id);
CREATE INDEX product_idx_03 ON car.product (origin, product_id);
</br></br>
-- Insert sample data
INSERT INTO car.product (
 product_id, product_name, sku, origin, color,
 category_id, price)
VALUES (
 'P00000001', 'Model K', 'S0001-20841-2233-331', 'USA', 'Black',
 'CT000001', 39999.99);
</br></br>
SELECT category_id, designer FROM car.category_designer;
</br></br>
SELECT
    p.product_id,
    p.product_name,
    p.price,
    p.sku,
    p.category_id,
    c.description AS category_description,
    ARRAY_AGG(cd.designer) AS designers
FROM car.product p
JOIN car.category c ON p.category_id = c.category_id
JOIN car.category_designer cd ON p.category_id = cd.category_id
GROUP BY p.product_id, p.product_name, p.price, p.sku, p.category_id, c.description;
</br></br>
SELECT
    p.product_id,
    p.product_name,
    p.price,
    p.sku,
    p.category_id,
    c.description AS category_description,
    cd.designer AS designers
FROM car.product p
JOIN car.category c ON p.category_id = c.category_id
JOIN car.category_designer cd ON p.category_id = cd.category_id;

</br></br>

p3.9</br>
-- Create the Order Header table under the car schema
CREATE TABLE car.order_header (
    order_no           VARCHAR(20) NOT NULL,
    customer_id        VARCHAR(20) REFERENCES car.customer (customer_id),
    order_dtm          TIMESTAMP(0),
    delivery_address_1 VARCHAR(30),
    delivery_address_2 VARCHAR(30),
    delivery_address_3 VARCHAR(30),
    delivery_address_4 VARCHAR(30),
    discount_rate      NUMERIC(5,2),
    order_net_total    MONEY,
    PRIMARY KEY (order_no, customer_id)
);
</br></br>
-- Create index
CREATE INDEX order_header_idx_01 ON car.order_header (order_no, customer_id);
</br></br>
-- Insert sample data
INSERT INTO car.order_header (
    order_no, customer_id, order_dtm, delivery_address_1, 
    discount_rate, order_net_total)
VALUES (
   'OR2023000001', 'C230000001', '2023-08-03 12:00:00', '123 Main St', 
   0.10, 71999.98);

</br></br></br>

p3.10</br>
-- Create the Order Detail table under the car schema
CREATE TABLE car.order_detail (
    order_no   VARCHAR(20) NOT NULL,
    product_id VARCHAR(20) REFERENCES car.product (product_id),
    qty        NUMERIC(11,2),
    unit_price NUMERIC(15,2),
    amount     NUMERIC(15,2),
    PRIMARY KEY (order_no, product_id)
);
</br></br>
-- Create index
CREATE INDEX order_detail_idx_01 ON car.order_detail (order_no, product_id);
</br></br>
-- Insert sample data
INSERT INTO car.order_detail (order_no, product_id, qty, unit_price, amount)
VALUES ('OR2023000001', 'P00000001', 2, 39999.99, 79999.98);
</br></br>


p3.11</br>
ALTER TABLE car.customer
ADD CONSTRAINT customer_tweeter_account_id_unique UNIQUE (tweeter_account_id);
</br></br>

-- Create the Tweets table under the car schema
CREATE TABLE car.tweet (
    tweet_message_id   VARCHAR(64) PRIMARY KEY,
    tweeter_account_id VARCHAR(64) REFERENCES car.customer(tweeter_account_id),
    content            TEXT,
    publish_dtm        TIMESTAMP(6),
    image              BYTEA,
    video              VARCHAR(100),
    url                VARCHAR(100)
);
</br></br>
-- Create index
CREATE INDEX tweet_idx_01 ON car.tweet (tweet_message_id, tweeter_account_id);
</br></br>
-- Insert sample data
INSERT INTO car.tweet (
 tweet_message_id, tweeter_account_id, 
 content, 
 publish_dtm, image, video, url)
VALUES (
'T000000001', '@thomassbright',
 'Excited to share our latest electric car model!', 
 '2023-08-03 12:00:00.000000', NULL, NULL, NULL);

</br></br></br>

p4.</br>
--Connect to your new database, about_x
\c about_x
</br></br>
CREATE TABLE t6 (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    description VARCHAR(100)
);
</br></br>
CREATE TABLE t7 (
    id INT PRIMARY KEY,
    t6_id INT,
    details VARCHAR(200),
    FOREIGN KEY (t6_id) REFERENCES t6(id)
);
</br></br>
INSERT INTO t6 (id, name, description)
VALUES (1, 'Item A', 'Description for Item A'),
       (2, 'Item B', 'Description for Item B'),
       (3, 'Item C', 'Description for Item C'),
       (4, 'Item D', 'Description for Item D'),
       (5, 'Item E', 'Description for Item E');
</br></br>
INSERT INTO t7 (id, t6_id, details)
VALUES (1, 1, 'Details for Item A'),
       (2, 2, 'Details for Item B'),
       (3, 1, 'Details for Item A'),
       (4, 3, 'Details for Item C'),
       (5, 2, 'Details for Item B');
</br></br>
\dt
</br></br></br>


p4.1</br>
--Connect to your new database, about_x
\c about_x
</br></br>
ALTER TABLE t6
ADD COLUMN new_column VARCHAR(50);
</br></br>
INSERT INTO t6 (id, name, description, new_column)
VALUES (6, 'Item F', 'Description for Item F', '600'),
       (7, 'Item G', 'Description for Item G', '700'),
       (8, 'Item H', 'Description for Item H', '800');
</br></br>
\d t7
</br></br>
ALTER TABLE t6
ALTER COLUMN new_column SET DATA TYPE INT USING new_column::INT;
</br></br>
ALTER TABLE t6
RENAME COLUMN new_column TO new_int;
</br></br>
\d t6
</br></br>
SELECT * FROM t6;
</br></br></br>


p4.2</br>
\c about_x
</br></br>
DROP TABLE t6;

</br></br></br>

p4.3</br>
\c about_x
</br></br>
DROP TABLE t6 CASCADE;
</br></br>
\d t7

</br></br></br>

p4.4</br>
--Connect to database about_x
</br>
\c about_x
</br></br>
--Create a new index set the order by publish date, then by account by message 
</br>
CREATE INDEX CONCURRENTLY tweet_idx_02 ON car.tweet (publish_dtm, tweeter_account_id, tweet_message_id);
</br></br></br>


p4.5</br>
ALTER INDEX car.tweet_idx_02 RENAME TO tweet_idx_02a;
</br></br>
-- Drop the existing index</br>
DROP INDEX car.tweet_idx_02a;
</br></br>
-- Create a new index with additional columns</br>
CREATE INDEX CONCURRENTLY tweet_idx_02 ON car.tweet (publish_dtm, tweet_message_id, tweeter_account_id);

</br></br></br>

p4.6</br>
\c about_x
</br></br>
CREATE VIEW space_trip_details AS
SELECT st.trip_id, sch.destination, sch.departure_dtm,
       c.first_name, c.last_name, 
       st.amount_paid
FROM space.space_trip st
JOIN car.customer c ON st.customer_id = c.customer_id
JOIN space.space_travel_schedule sch ON st.trip_id = sch.trip_id;
</br></br>
SELECT * FROM space_trip_details LIMIT 1;
</br></br>
--Add new column to view: drop the view and create view again</br>
DROP VIEW space_trip_details;
</br></br>
CREATE VIEW space_trip_details AS
SELECT st.trip_id, sch.destination, sch.departure_dtm, sch.return_dtm,
       c.first_name, c.last_name,
       st.amount_paid
FROM space.space_trip st
JOIN car.customer c ON st.customer_id = c.customer_id
JOIN space.space_travel_schedule sch ON st.trip_id = sch.trip_id;
</br></br>
SELECT * FROM space_trip_details LIMIT 1;
</br></br>
DROP VIEW space_trip_details;
</br></br></br>


p4.7</br>
-- Order number column</br>
COMMENT ON COLUMN car.order_header.order_no IS 'Unique identifier for each order.';
</br></br>
-- Discount rate column</br>
COMMENT ON COLUMN car.order_header.discount_rate IS 'Percentage discount applied to the whole order.';
</br></br>
-- Order net total column</br>
COMMENT ON COLUMN car.order_header.order_net_total IS 'Total net amount of the order after discounts, = SUM(order_detail.amount) - SUM(order_detail.amount) * order_header.discount_rate ';

</br></br></br>

p5.</br>
\c about_x
</br></br>
INSERT INTO car.tweet (
  tweet_message_id, tweeter_account_id, 
  content, 
  publish_dtm, image, video, url)
VALUES (
  'T000000002', 'C230000001', 
  ' Data manipulation in a database refers to the process of adding, altering, retrieving, or deleting data stored within the database. ', 
  '2023-08-05 15:00:00.000000', NULL, NULL, NULL);
</br></br></br>


p5.1</br>
\c about_x
</br></br>
INSERT INTO car.tweet (
  tweet_message_id,
  tweeter_account_id, 
  content, 
  publish_dtm,
  image,
  video,
  url)
VALUES (
  'T000000002',
  '@thomassbright', 
  ' Data manipulation in a database refers to the process of adding, altering, retrieving, or deleting data stored within the database. ', 
  '2023-08-05 15:00:00.000000',
  NULL,    
  'https://www.youtube.com/watch?v=T000000002', 
  'https://twitter.com/your_username/status/T000000002'
);
</br></br>
SELECT * FROM car.tweet WHERE tweet_message_id ='T000000003';
</br></br>
SELECT
     c.customer_id,
     c.first_name,
     c.last_name,
     oh.order_no,
     oh.order_dtm,
     od.product_id,
     od.unit_price,
     p.product_name,
     p.price AS unit_price,
     cat.category_id,
     cat.description AS category_description,
     od.qty AS total_quantity
FROM car.customer AS c
JOIN car.order_header AS oh ON c.customer_id = oh.customer_id
JOIN car.order_detail AS od ON oh.order_no = od.order_no
JOIN car.product AS p ON od.product_id = p.product_id
JOIN car.category AS cat ON p.category_id = cat.category_id
ORDER BY c.customer_id, oh.order_no, od.product_id;

</br></br></br>

p5.2</br>
\c about_x
</br></br>
UPDATE car.order_detail
SET    unit_price = 34999.99,
       amount = qty * 34999.99
WHERE  order_no = 'OR2023000001' AND product_id = 'P00000001';
</br></br>
SELECT * FROM   car.order_detail 
WHERE  order_no = 'OR2023000001' AND product_id = 'P00000001';
</br></br>
SELECT COUNT(1) FROM car.tweet;
</br></br>
DELETE FROM car.tweet
WHERE tweet_message_id = 'T000000001';
</br></br>
SELECT COUNT(1) FROM car.tweet;
</br></br></br>


p5.3</br>
SELECT COUNT(1) FROM car.tweet;
</br></br>
DELETE FROM car.tweet
WHERE tweet_message_id = 'T000000001';
</br></br>
SELECT COUNT(1) FROM car.tweet;
</br></br>
--Merge with Insert or Update</br>
MERGE INTO car.tweet AS target
USING (
        SELECT
          'T000000003' AS tweet_message_id,
          '@thomassbright' AS tweeter_account_id,
          'Check out MERGE as it is cool!' AS content,
          TIMESTAMP '2023-08-04 10:30:00.000000' AS publish_dtm,
          NULL::bytea AS image,
          'https://www.youtube.com/watch?v=your_video_id' AS video,
          'https://twitter.com/your_username/status/your_tweet_id' AS url
      ) AS source
ON (target.tweet_message_id = source.tweet_message_id)
WHEN MATCHED THEN
     UPDATE SET
        content = source.content,
        publish_dtm = source.publish_dtm,
        image = source.image,
        video = source.video,
        url = source.url
WHEN NOT MATCHED THEN
    INSERT (tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
    VALUES (source.tweet_message_id, source.tweeter_account_id, source.content,   
            source.publish_dtm, source.image, source.video, source.url);
</br></br>
SELECT * FROM car.tweet WHERE tweet_message_id = 'T000000003';
</br></br>
--let us change some sample values, and run the MERGER again</br>
MERGE INTO car.tweet AS target
USING (
        SELECT
          'T000000003' AS tweet_message_id,
          '@thomassbright' AS tweeter_account_id,
          'Check out MERGE as it is cool!' AS content,
          TIMESTAMP '2023-09-02 11:30:00.000000' AS publish_dtm,
          NULL::bytea AS image,
          'https://www.youtube.com/watch?v=T000000003' AS video,
          'https://twitter.com/your_username/status/T000000003' AS url
      ) AS source
ON (target.tweet_message_id = source.tweet_message_id)
WHEN MATCHED THEN
    UPDATE SET
        content = source.content,
        publish_dtm = source.publish_dtm,
        image = source.image,
        video = source.video,
        url = source.url
WHEN NOT MATCHED THEN
    INSERT (tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
    VALUES (source.tweet_message_id, source.tweeter_account_id, source.content, 
            source.publish_dtm, source.image, source.video, source.url);
</br></br>
SELECT * FROM car.tweet WHERE tweet_message_id = 'T000000003';

</br></br></br>

p5.4</br>
\c about_x
</br></br>
CREATE TABLE car.tweet_shared (
    tweet_message_id   VARCHAR(64) PRIMARY KEY,
    tweeter_account_id VARCHAR(64) REFERENCES car.customer(tweeter_account_id),
    content            TEXT,
    publish_dtm        TIMESTAMP(6),
    image              BYTEA,
    video              VARCHAR(100),
    url                VARCHAR(100)
);
</br></br>
--Let us truncate the source table and insert new records into it again
TRUNCATE car.tweet;
</br></br>
INSERT INTO car.tweet (
 tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
VALUES (
'T000000001', '@thomassbright',
 'Excited to share our latest electric car model!', 
 '2023-08-03 12:00:00.000000', NULL, NULL, NULL);
</br></br>
INSERT INTO car.tweet (
 tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
VALUES (
'T000000002', '@thomassbright',
 'Advanced Table Synchronization!', 
 '2023-09-01 10:22:00.000000', NULL,    
 'https://www.youtube.com/watch?v=T000000002', 
 'https://twitter.com/your_username/status/T000000002');

</br></br>

INSERT INTO car.tweet (
 tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
VALUES (
'T000000003', '@thomassbright',
 'let us check the result!', 
 '2023-09-02 11:22:00.000000', NULL,    
 'https://www.youtube.com/watch?v=T000000003', 
 'https://twitter.com/your_username/status/T000000003');

</br></br>

-- Synchronize these two tables</br>

INSERT INTO car.tweet_shared (
  tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
SELECT
    source.tweet_message_id,
    source.tweeter_account_id,
    source.content,
    source.publish_dtm,
    source.image,
    source.video,
    source.url
FROM car.tweet source
ON CONFLICT (tweet_message_id) DO UPDATE
    SET
        tweeter_account_id = excluded.tweeter_account_id,
        content = excluded.content,
        publish_dtm = excluded.publish_dtm,
        image = excluded.image,
        video = excluded.video,
        url = excluded.url;

</br></br>

-- Delete records not present in the source</br>

DELETE FROM car.tweet_shared target
WHERE NOT EXISTS (
    SELECT 1
    FROM car.tweet source
    WHERE target.tweet_message_id = source.tweet_message_id
);
</br></br>

SELECT * FROM car.tweet;
</br></br>

SELECT * FROM car.tweet_shared;
</br></br>

--Delete a row in source and update a row in source table, then synchronize them again</br>

DELETE FROM car.tweet WHERE tweet_message_id = 'T000000001';
</br></br>

UPDATE car.tweet SET
  publish_dtm = '2023-09-03 10:22:00.000000',
  content     = 'Advanced Table Synchronization – Updated!'
WHERE tweet_message_id = 'T000000002';

</br></br>

INSERT INTO car.tweet_shared (
  tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
SELECT
    source.tweet_message_id,
    source.tweeter_account_id,
    source.content,
    source.publish_dtm,
    source.image,
    source.video,
    source.url
FROM car.tweet source
ON CONFLICT (tweet_message_id) DO UPDATE
    SET
        tweeter_account_id = excluded.tweeter_account_id,
        content = excluded.content,
        publish_dtm = excluded.publish_dtm,
        image = excluded.image,
        video = excluded.video,
        url = excluded.url;

</br></br>

-- Delete records not present in the source</br>

DELETE FROM car.tweet_shared target
WHERE NOT EXISTS (
    SELECT 1
    FROM car.tweet source
    WHERE target.tweet_message_id = source.tweet_message_id
);

</br></br>

SELECT * FROM car.tweet;

</br></br>

SELECT * FROM car.tweet_shared;

</br></br></br>

p5.5</br>
\c about_x

</br></br>

BEGIN; -- Start the transaction 

</br></br>

-- Insert new record into order_header</br>
INSERT INTO car.order_header (
    order_no, customer_id, order_dtm, delivery_address_1, discount_rate, order_net_total
)
VALUES (
    'O00000002', 'C230000001', '2023-08-15 14:00:00', '456 Elm St',  0.05,  113999.97
);

</br></br>

-- Insert corresponding record into order_detail</br>
INSERT INTO car.order_detail (
    order_no, product_id, qty, unit_price, amount
)
VALUES (
    'O00000002', 'P00000001', 3, 39999.99, 119999.97
);

</br></br>

-- Commit the transaction if both inserts succeed</br>
COMMIT;

</br></br>

SELECT * FROM car.order_detail;

</br></br>

SELECT order_no, customer_id, order_dtm, delivery_address_1 FROM car.order_header;

</br></br></br>

p5.6</br>
\c about_x

</br></br>

BEGIN; -- Start the transaction

</br></br>

--Update customer's address</br>

UPDATE car.customer
SET    address_1 = '789 Oak St'
WHERE  customer_id = 'C230000001';

</br></br>

--Update order_header's delivery address</br>

UPDATE car.order_header
SET    delivery_address_1 = '789 Oak St'
WHERE  order_no = 'O00000002';

</br></br>

--Commit the transaction if both updates succeed</br>

COMMIT;

</br></br>

SELECT customer_id, address_1 
FROM car.customer;

</br></br>

SELECT order_no, customer_id, delivery_address_1 
FROM car.order_header
WHERE  order_no = 'O00000002';

</br></br></br>

p5.7</br>
--Connect to your new database, about_x</br>
\c about_x

</br></br>

TRUNCATE t6;

</br></br>

p5.8</br>
--Connect to your new database, about_x</br>
\c about_x

</br></br>

TRUNCATE t7 CASCADE;

</br></br>

TRUNCATE t6 CASCADE;

</br></br>


p5.9</br>
--Connect to your new database, about_x</br>

\c about_x

</br></br>

--Describe an existing table car.tweet</br>

\d car.tweet

</br></br>

--Create a trigger on INSERT, which will prevent content is null </br>

CREATE OR REPLACE FUNCTION prevent_null_content()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.content IS NULL THEN
        RAISE EXCEPTION 'Content cannot be null';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

</br></br>

CREATE TRIGGER check_content_before_insert BEFORE INSERT ON car.tweet
FOR EACH ROW EXECUTE FUNCTION prevent_null_content();

</br></br>
--Create a trigger on UPDATE, which will prevent content is null </br>

CREATE OR REPLACE FUNCTION prevent_null_content_update()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.content IS NULL THEN
        RAISE EXCEPTION 'Content cannot be set to null';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

</br></br>

CREATE TRIGGER check_content_before_update BEFORE UPDATE ON car.tweet
FOR EACH ROW EXECUTE FUNCTION prevent_null_content_update();

</br></br>
--Now let's test the TRIGGER on INSERT</br>

INSERT INTO car.tweet(
tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
VALUES ('T000000001', '@user123', NULL, '2023-08-05 15:00:00', NULL, NULL, 'https://twitter.com/user123/status/123456');

</br></br>

SELECT  * FROM car.tweet;

</br></br>

--Now let's test the TRIGGER on UPDATE</br>
UPDATE car.tweet
SET content = NULL
WHERE tweet_message_id = 'T000000002';

</br></br></br>

p6.</br>

\c about_x

</br></br>

SELECT c.customer_id, c.first_name, c.last_name, SUM(oh.order_net_total) AS total_amount
FROM car.customer c
JOIN car.order_header oh ON c.customer_id = oh.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name;

</br></br>

p6.1</br>

\c about_x

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000002', 'Classic Watch', 'S0002-12345', 'Switzerland', 'Silver', 'CT000001', 599.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000003', 'Leather Bag', 'S0003-67890', 'Italy', 'Brown', 'CT000003', 249.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000004', 'Wireless Headphones', 'S0004-56789', 'USA', 'Black', 'CT000004', 149.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000005', 'Smartphone', 'S0005-23456', 'China', 'Gold', 'CT000001', 699.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000006', 'Laptop', 'S0006-34567', 'USA', 'Silver', 'CT000001', 999.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000007', 'Sports Shoes', 'S0007-45678', 'Germany', 'Blue', 'CT000001', 89.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000008', 'HD Television', 'S0008-78901', 'Japan', 'Black', 'CT000001', 799.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000009', 'Designer Sunglasses', 'S0009-89012', 'Italy', 'Brown', 'CT000001', 199.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000010', 'Fitness Tracker', 'S0010-90123', 'USA', 'Black', 'CT000001', 49.99);

</br></br>

INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES ('P00000011', 'Coffee Maker', 'S0011-01234', 'Switzerland', 'Silver', 'CT000001', 79.99);

</br></br>

SELECT p.category_id,
    MAX(p.price::NUMERIC) AS max_price,
    MIN(p.price::NUMERIC) AS min_price,
    AVG(p.price::NUMERIC) AS avg_price,
    COUNT(product_id),
    VARIANCE(p.price::NUMERIC) AS variance_price,
    STDDEV(p.price::NUMERIC) AS stddve_price,
    STDDEV_POP(p.price::NUMERIC) AS stddve_pop_price,
    STDDEV_SAMP(p.price::NUMERIC) AS stddve_samp_price
FROM car.product p
GROUP BY p.category_id
ORDER BY p.category_id;

</br></br>

p6.2</br>

\c about_x

</br></br>

\d car.order_detail

</br></br>

SELECT
    SUM(amount) AS  total_amount,
    REGR_COUNT(qty, amount) AS num_valid_rows,
    REGR_AVGX(qty, amount) AS regr_avg_qty,
    REGR_AVGY(qty, amount) AS regr_avg_amount,
    REGR_SLOPE(qty, amount) AS regr_slope,
    REGR_INTERCEPT(qty, amount) AS regr_intercept,
    REGR_R2(qty, amount) AS regr_r_squared,
    REGR_SXX(qty, amount) AS regr_sum_squares_x,
    REGR_SYY(qty, amount) AS regr_sum_squares_y,
    REGR_SXY(qty, amount) AS regr_sum_products_xy,
    VAR_POP(amount) AS var_pop_amount,
    VAR_SAMP(amount) AS var_samp_amount,
    CORR(qty, amount) AS correlation_qty_amount,
    COVAR_POP(qty, amount) AS covar_pop_qty_amount,
    COVAR_SAMP(qty, amount) AS covar_samp_qty_amount
FROM car.order_detail;

</br></br>

p6.3</br>
\c about_x

--Describe the table structure of car.product
\d car.product

--Describe the table structure of car.category
\d car.category

SELECT
    p.product_id,
    p.product_name,
    p.price,
    p.sku,
    p.category_id,
    c.description AS category_description,
    ARRAY_AGG(cd.designer) AS designers,
    STRING_AGG(cd.designer, ', ') AS concatenated_designers,
    BOOL_AND(p.price::numeric > 0) AS all_positive_prices,
    BOOL_OR(p.price::numeric > 100) AS any_price_above_100,
    EVERY(p.price::numeric > 50) AS all_prices_above_50
FROM car.product p
JOIN car.category c ON p.category_id = c.category_id
JOIN car.category_designer cd ON p.category_id = cd.category_id
WHERE p.product_id = 'P00000001'
GROUP BY p.product_id, p.product_name, p.price, p.sku, p.category_id, c.description;



p6.4
\c about_x

SELECT oh.order_no, oh.order_net_total
FROM car.order_header oh
WHERE oh.order_net_total::numeric > (SELECT AVG(order_net_total::numeric) FROM car.order_header);



p6.5
\c about_x

WITH OrderCounts AS (
    SELECT customer_id, COUNT(*) AS order_count
    FROM car.order_header
    GROUP BY customer_id
)
SELECT c.customer_id, c.first_name, c.last_name, COALESCE(oc.order_count, 0) AS order_count
FROM car.customer c
LEFT JOIN OrderCounts oc ON c.customer_id = oc.customer_id;



p6.6
\c about_x

-- Insert more sample data

-- Inserting into car.customer
INSERT INTO car.customer (customer_id, title, first_name, middle_name, last_name, email, phone, address_1, address_2, address_3, address_4, city, country, postal_code, tweeter_account_id)
VALUES
    ('C00000002', 'Ms.', 'Jane', '', 'Johnson', 'jane@example.com', '+9876543210', '456 Elm St', '', '', '', 'Townsville', 'Countryland', '54321', '@janejohnson'),
    -- Add 3 more records with similar structure
    ('C00000003', 'Dr.', 'Michael', '', 'Williams', 'michael@example.com', '+1122334455', '789 Oak St', '', '', '', 'Villagetown', 'Countryland', '67890', '@drmike'),
    ('C00000004', 'Prof.', 'Emily', '', 'Brown', 'emily@example.com', '+5544332211', '101 Pine St', '', '', '', 'Citytown', 'Countryland', '45678', '@profemily'),
    ('C00000005', 'Mrs.', 'Daniel', '', 'Miller', 'daniel@example.com', '+3344556677', '222 Maple St', '', '', '', 'Suburbville', 'Countryland', '98765', '@mrsdaniel');
    

-- Inserting into car.category
INSERT INTO car.category (category_id, description)
VALUES
    ('CT000002', 'Car Charger'),
    -- Add 3 more records with different categories
    ('CT000003', 'Battery'),
    ('CT000004', 'Accessory'),
    ('CT000005', 'Cleaning Kid');

-- Inserting into car.product
INSERT INTO car.product (product_id, product_name, sku, origin, color, category_id, price)
VALUES
    ('P00000002', 'Quick Charge', 'SKU002', 'China', 'Blue', 'CT000002', '$699.99'),
    -- Add 3 more records with different products
    ('P00000003', 'Super Battery Pack', 'SKU003', 'Italy', 'Brown', 'CT000003', '$19999.99'),
    ('P00000004', 'Car Cam', 'SKU004', 'UK', 'Various', 'CT000004', '$399.99'),
    ('P00000005', 'Easy Clean', 'SKU005', 'France', 'Red', 'CT000005', '$69.99');

-- Inserting into car.category_designer
INSERT INTO car.category_designer (category_id, designer)
VALUES
    ('CT000002', 'Peter'),
    -- Add 3 more records with different designers
    ('CT000003', 'Thomas'),
    ('CT000004', 'Eddie'),
    ('CT000005', 'Gary');

-- Inserting into car.order_header
INSERT INTO car.order_header (order_no, customer_id, order_dtm, delivery_address_1, discount_rate, order_net_total)
VALUES
    ('OR00000001', 'C00000001', '2023-08-01', '123 Main St', 0.1, (4 * 39999.99) - (4 * 39999.99) * 0.1),
    ('OR00000002', 'C00000002', '2023-08-02', '456 Elm St', 0.05, (5 * 699.99) - (5 * 699.99) * 0.05),
    ('OR00000003', 'C00000003', '2023-08-03', '789 Oak St', 0.2, (1 * 19999.99) - (1 * 19999.99) * 0.2),
    ('OR00000004', 'C00000004', '2023-08-04', '101 Pine St', 0.15, (3 * 399.99) - (3 * 399.99) * 0.15),
    ('OR00000005', 'C00000005', '2023-08-05', '222 Maple St', 0.1, (2 * 69.99) - (2 * 69.99) * 0.1);

-- Inserting into car.order_detail
INSERT INTO car.order_detail (order_no, product_id, qty, unit_price, amount)
VALUES
    ('OR00000001', 'P00000001', 4, 39999.99, 159999.96),
    ('OR00000002', 'P00000002', 5, 699.99, 3499.95),
    ('OR00000003', 'P00000003', 1, 19999.99, 19999.99),
    ('OR00000004', 'P00000004', 3, 399.99, 1199.97),
    ('OR00000005', 'P00000005', 2, 69.99, 139.98);

SELECT c.customer_id, c.first_name, c.last_name, oh.order_no,
       SUM(oh.order_net_total) 
       OVER (PARTITION BY c.customer_id 
             ORDER BY oh.order_no) AS cumulative_total
FROM car.customer c
JOIN car.order_header oh ON c.customer_id = oh.customer_id
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
ORDER BY c.customer_id, oh.order_no;

SELECT DISTINCT p.category_id, 
       SUM(od.amount) OVER (PARTITION BY p.category_id) AS cumulative_total_by_category
FROM car.order_detail od
JOIN car.product p ON od.product_id = p.product_id
JOIN car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
ORDER BY p.category_id;

SELECT DISTINCT cd.designer, SUM(od.amount)
       OVER (PARTITION BY cd.designer ORDER BY cd.designer) AS cumulative_total_by_designer
FROM car.order_detail od 
JOIN car.product p ON od.product_id = p.product_id
JOIN car.category_designer cd ON p.category_id = cd.category_id
JOIN car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
ORDER BY cd.designer;



p6.7
-- Create more sales data for year 2022
-- Inserting into car.order_header
INSERT INTO car.order_header (order_no, customer_id, order_dtm, delivery_address_1, discount_rate, order_net_total)
VALUES
    ('2200000001', 'C00000001', '2022-07-01', '123 Main St', 0.1, (5 * 39999.99) - (5 * 39999.99) * 0.1),
    ('2200000002', 'C00000002', '2022-07-02', '456 Elm St', 0.05, (2 * 699.99) - (2 * 699.99) * 0.05),
    ('2200000003', 'C00000003', '2023-07-03', '789 Oak St', 0.2, (4 * 19999.99) - (4 * 19999.99) * 0.2),
    ('2200000004', 'C00000004', '2022-07-04', '101 Pine St', 0.15, (1 * 399.99) - (1 * 399.99) * 0.15),
    ('2200000005', 'C00000005', '2022-07-05', '222 Maple St', 0.1, (1 * 69.99) - (1 * 69.99) * 0.1);

-- Inserting into car.order_detail
INSERT INTO car.order_detail (order_no, product_id, qty, unit_price, amount)
VALUES
    ('2200000001', 'P00000001', 3, 39999.99, 119999.97),
    ('2200000002', 'P00000002', 2, 699.99, 1399.98),
    ('2200000003', 'P00000003', 4, 19999.99, 79999.96),
    ('2200000004', 'P00000004', 1, 399.99, 399.99),
    ('2200000005', 'P00000005', 1, 69.99, 69.99);

SELECT 
    p.product_name, EXTRACT(YEAR FROM oh.order_dtm) AS order_year,
    SUM(od.amount) AS total_sales,
    LAG(SUM(od.amount)) OVER (PARTITION BY p.category_id ORDER BY EXTRACT(YEAR FROM oh.order_dtm)) AS previous_year_sales, 
    LEAD(SUM(od.amount)) OVER (PARTITION BY p.category_id ORDER BY EXTRACT(YEAR FROM oh.order_dtm)) AS next_year_sales
FROM car.order_detail od 
JOIN car.product p ON od.product_id = p.product_id
JOIN car.order_header oh ON od.order_no = oh.order_no
GROUP BY EXTRACT(YEAR FROM oh.order_dtm), p.product_id
ORDER BY p.product_id, order_year;



p6.8
SELECT designer, total_sales, ROW_NUMBER() OVER (ORDER BY total_sales DESC) AS sales_rank
FROM (
    SELECT cd.designer, SUM(od.amount) AS total_sales
    FROM car.order_header oh
    JOIN car.order_detail od ON oh.order_no = od.order_no
    JOIN car.product p ON od.product_id = p.product_id
    JOIN car.category_designer cd ON p.category_id = cd.category_id
    WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
    GROUP BY cd.designer
) AS designer_sales
ORDER BY sales_rank;



p6.9
SELECT
    p.product_name,
    SUM(od.amount) AS total_sales,
    RANK() OVER (ORDER BY SUM(od.amount) DESC) AS sales_rank,
    DENSE_RANK() OVER (ORDER BY SUM(od.amount) DESC) AS dense_sales_rank
FROM car.order_detail od
JOIN car.product p ON od.product_id = p.product_id
JOIN car.category_designer cd ON p.category_id = cd.category_id
JOIN car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
GROUP BY p.product_name
ORDER BY sales_rank;



p6.10
SELECT DISTINCT ON (cd.designer) cd.designer,
FIRST_VALUE(oh.order_dtm) OVER (PARTITION BY cd.designer 
   ORDER BY oh.order_dtm) AS first_order_date,
LAST_VALUE(oh.order_dtm) OVER (PARTITION BY cd.designer 
   ORDER BY oh.order_dtm ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_order_date,
SUM(od.amount) OVER (PARTITION BY cd.designer) AS total_amount
FROM  car.order_header oh
JOIN  car.order_detail od ON oh.order_no = od.order_no
JOIN  car.product p ON od.product_id = p.product_id
JOIN  car.category_designer cd ON p.category_id = cd.category_id
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
ORDER BY cd.designer, last_order_date;



p6.11
SELECT p.product_name, EXTRACT(YEAR FROM oh.order_dtm) AS order_year,
    SUM(od.amount) AS total_sales,
    NTILE(3) OVER (PARTITION BY EXTRACT(YEAR FROM oh.order_dtm) ORDER BY SUM(od.amount) DESC) AS sales_quartile
FROM  car.order_detail od
JOIN  car.product p ON od.product_id = p.product_id
JOIN  car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
GROUP BY p.product_name, EXTRACT(YEAR FROM oh.order_dtm)
ORDER BY sales_quartile, total_sales DESC;

SELECT p.product_name, EXTRACT(YEAR FROM oh.order_dtm) AS order_year,
    SUM(od.amount) AS total_sales,
    NTILE(4) OVER (PARTITION BY EXTRACT(YEAR FROM oh.order_dtm) ORDER BY SUM(od.amount) DESC) AS sales_quartile
FROM  car.order_detail od
JOIN  car.product p ON od.product_id = p.product_id
JOIN  car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
GROUP BY p.product_name, EXTRACT(YEAR FROM oh.order_dtm)
ORDER BY sales_quartile, total_sales DESC;



p6.12
SELECT p.product_name, EXTRACT(YEAR FROM oh.order_dtm) AS order_year,
    SUM(od.amount) AS total_sales,
    PERCENT_RANK() OVER (PARTITION BY EXTRACT(YEAR FROM oh.order_dtm) ORDER BY SUM(od.amount)) AS percent_rank,
    CUME_DIST() OVER (PARTITION BY EXTRACT(YEAR FROM oh.order_dtm) ORDER BY SUM(od.amount)) AS cume_dist
FROM car.order_detail od
JOIN car.product p ON od.product_id = p.product_id
JOIN car.order_header oh ON od.order_no = oh.order_no
WHERE EXTRACT(YEAR FROM oh.order_dtm) = 2023
GROUP BY p.product_name, EXTRACT(YEAR FROM oh.order_dtm)
ORDER BY order_year, percent_rank;



p6.13
SELECT
    c.city,
    c.country,
    ct.description AS category,
    cd.designer,
    SUM(od.amount) AS total_sales_amount
FROM car.order_detail od
JOIN car.order_header oh ON od.order_no = oh.order_no
JOIN car.customer c ON oh.customer_id = c.customer_id
JOIN car.product p ON od.product_id = p.product_id
JOIN car.category ct ON p.category_id = ct.category_id
JOIN car.category_designer cd ON ct.category_id = cd.category_id
GROUP BY c.city, c.country, ct.description, cd.designer
ORDER BY c.country, c.city, ct.description, cd.designer;



p6.14
SELECT
    c.city,
    c.country,
    ct.description AS category,
    cd.designer,
    SUM(od.amount) AS total_sales_amount
FROM car.order_detail od
JOIN car.order_header oh ON od.order_no = oh.order_no
JOIN car.customer c ON oh.customer_id = c.customer_id
JOIN car.product p ON od.product_id = p.product_id
JOIN car.category ct ON p.category_id = ct.category_id
JOIN car.category_designer cd ON ct.category_id = cd.category_id
GROUP BY
    ROLLUP ( c.city, c.country, ct.description, cd.designer)
ORDER BY     c.country, c.city, ct.description, cd.designer;



p6.15
SELECT
    c.country,
    c.city,
    ct.description AS category,
    SUM(od.amount) AS total_sales_amount
FROM    car.order_detail od
JOIN    car.order_header oh ON od.order_no = oh.order_no
JOIN    car.customer c ON oh.customer_id = c.customer_id
JOIN    car.product p ON od.product_id = p.product_id
JOIN    car.category ct ON p.category_id = ct.category_id
JOIN    car.category_designer cd ON ct.category_id = cd.category_id
GROUP BY
    GROUPING SETS (c.city, c.country, ct.description)
ORDER BY
    c.country, c.city, ct.description;



p6.16
SELECT
    c.country,
    c.city,
    ct.description AS category,
    SUM(od.amount) AS total_sales_amount
FROM    car.order_detail od
JOIN    car.order_header oh ON od.order_no = oh.order_no
JOIN    car.customer c ON oh.customer_id = c.customer_id
JOIN    car.product p ON od.product_id = p.product_id
JOIN    car.category ct ON p.category_id = ct.category_id
JOIN    car.category_designer cd ON ct.category_id = cd.category_id
GROUP BY
    CUBE (c.city, c.country, ct.description)
ORDER BY
    c.country, c.city, ct.description;



p6.17
\c about_x

--Create a new table with JSON Data type, we will JSON to store semi-structured data
CREATE TABLE car.tweet_comment (
    comment_id VARCHAR(64),
    comment_dtm TIMESTAMP(6),
    comment JSON,
    tweet_message_id VARCHAR(64) REFERENCES car.tweet(tweet_message_id)
);

--Insert more sample data
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES
    ('tweet001', '@thomassbright', 'Excited about our new product launch! #innovation', '2023-07-01 10:00:00.000000'),
    ('tweet002', '@thomassbright', 'Check out the features of our Super Battery Pack. #technology', '2023-07-02 12:30:00.000000'),
    ('tweet003', '@thomassbright', 'Thrilled to see the positive reviews for our latest product. #customerfeedback', '2023-07-03 15:45:00.000000'),
    ('tweet004', '@thomassbright', 'Join us for an interactive webinar on our new products. #webinar', '2023-07-04 09:15:00.000000'),
    ('tweet005', '@thomassbright', 'Our Super Battery Pack is now available for purchase! #productlaunch', '2023-07-05 11:30:00.000000'),
    ('tweet006', '@thomassbright', 'Exciting times ahead as we expand our product lineup. #growth', '2023-07-06 14:00:00.000000'),
    ('tweet007', '@thomassbright', 'Stay tuned for a special discount on our products. #specialoffer', '2023-07-07 16:20:00.000000'),
    ('tweet008', '@thomassbright', 'Thank you to all our loyal customers for your support! #gratitude', '2023-07-08 18:45:00.000000'),
    ('tweet009', '@thomassbright', 'Learn how our Super Battery Pack is changing the industry. #innovation', '2023-07-09 20:10:00.000000'),
    ('tweet010', '@thomassbright', 'Visit our website to explore the full range of our products. #website', '2023-07-10 22:30:00.000000');

INSERT INTO car.tweet_comment (comment_id, comment_dtm, comment, tweet_message_id)
VALUES
    ('comment006', '2023-09-02 11:30:00.000000', '{"text": "Looking forward to the results!"}', 'T000000003'),
    ('comment007', '2023-09-03 12:00:00.000000', '{"text": "Thanks for the update!"}', 'T000000002'),
    ('comment008', '2023-07-01 10:30:00.000000', '{"text": "This is awesome!"}', 'tweet001'),
    ('comment009', '2023-07-02 13:00:00.000000', '{"text": "I want one too!"}', 'tweet002'),
    ('comment010', '2023-07-03 16:30:00.000000', '{"text": "Impressive product!, I ordered Super Battery Pack"}', 'tweet002'),
    ('comment011', '2023-07-03 16:30:00.000000', '{"text": "Impressive product!, I ordered Super Battery Pack"}', 'tweet002');



p6.18
--Select Tweet comments
SELECT comment_dtm, c.comment->>'text' as comments FROM car.tweet_comment c;

--Select Tweet comments
SELECT comment_dtm, c.comment->>'text' as comments 
FROM   car.tweet_comment c
WHERE  LOWER(c.comment->>'text') LIKE '%battery%';

SELECT p.product_id
FROM   car.product p
JOIN   car.tweet_comment c ON POSITION('battery' IN LOWER(p.product_name)) > 0
WHERE  LOWER(c.comment->>'text') LIKE '%battery%';

SELECT
  oh.order_dtm,
  p.product_name,
  od.product_id,
  od.amount
FROM  car.order_header oh
JOIN  car.order_detail od ON oh.order_no = od.order_no
JOIN  car.product p ON od.product_id = p.product_id
WHERE od.product_id IN ( 
  SELECT p.product_id
  FROM   car.product p
  JOIN   car.tweet_comment c ON POSITION('battery' IN LOWER(p.product_name)) > 0
  WHERE LOWER(c.comment->>'text') LIKE '%battery%');

SELECT
     tc.comment_text AS tweet_comment, tc.comment_dtm,
     oh.order_dtm, p.product_name, od.product_id, od.amount
FROM car.order_header oh
JOIN car.order_detail od ON oh.order_no = od.order_no
JOIN car.product p ON od.product_id = p.product_id
JOIN (
    SELECT DISTINCT p.product_id, c.comment->>'text' AS comment_text, c.comment_dtm
    FROM   car.product p
    JOIN   car.tweet_comment c ON POSITION('battery' IN LOWER(p.product_name)) > 0
    WHERE  LOWER(c.comment->>'text') LIKE '%battery%'
      ) tc ON tc.product_id = od.product_id
WHERE od.product_id IN (
    SELECT p.product_id
    FROM   car.product p
    JOIN   car.tweet_comment c ON POSITION('battery' IN LOWER(p.product_name)) > 0
    WHERE  LOWER(c.comment->>'text') LIKE '%battery%'
);



p6.19
\c about_x

\d car.tweet 



p6.20
\c about_x

--There are 12 tweets, only 2 of them contain valid URL
--Retrieve records that contain valid URL
SELECT regexp_replace(url, E'[^https?://[^\s]+]', '', 'g') AS full_urls
FROM   car.tweet
WHERE  url ~ E'https?://[^\s]+';



p6.21
\c about_x

--Insert a sample record
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES (
'T20230907123456789', '@thomassbright', 'I have compared the products and found this one is interesting, feel free to contact me by email if you want know my comparison result, my email is thomas@mythomasbrighttest.com.', '2023-08-01 12:00:00');

--Extract email address from free form text
SELECT 
 REGEXP_MATCHES(content, E'[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}', 'g') AS   
 email_addresses
FROM car.tweet
WHERE content ~ E'[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}';



p6.22
\c about_x


SELECT comment_id,
   array_length(regexp_split_to_array(json_extract_path_text(comment, 'text')::text, E'\\s+'), 1) 
   AS word_count
FROM car.tweet_comment
ORDER BY array_length(regexp_split_to_array(json_extract_path_text(comment, 'text')::text, E'\\s+'), 1) DESC;



p6.23
\c about_x


SELECT comment_id,
   array_length(regexp_split_to_array(json_extract_path_text(comment, 'text')::text, E'\\s+'), 1) 
   AS word_count
FROM car.tweet_comment
ORDER BY array_length(regexp_split_to_array(json_extract_path_text(comment, 'text')::text, E'\\s+'), 1) DESC;

SELECT content 
FROM   car.tweet 
WHERE  tweet_message_id = 'T20230907123456789';



p6.24
\c about_x

SELECT *
FROM car.tweet
WHERE content ~ E'#\\w+';



p6.25
\c about_x

SELECT * FROM car.tweet WHERE content ~ E'@[A-Za-z0-9_]+';



p6.26
\c about_x

SELECT tweet_message_id, comment->>'text' AS comment
FROM   car.tweet_comment
WHERE  TO_TSVECTOR('english', comment->>'text') @@ TO_TSQUERY('Super');



p6.27
\c about_x

-- Inserting a tweet with hexadecimal data
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES ('tweet011', '@thomassbright', E'\\x48656c6c6f20776f726c6421', '2023-08-01 12:00:00');

-- Inserting another tweet with hexadecimal data
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES ('tweet012', '@thomassbright', E'\\x5468697320697320616e6f7468657220747765657421', '2023-08-02 12:00:00');

-- Inserting a tweet with regular text content
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES ('tweet013', '@thomassbright', 'This is a regular text tweet.', '2023-08-03 12:00:00');

-- Inserting a tweet with more hexadecimal data
INSERT INTO car.tweet (tweet_message_id, tweeter_account_id, content, publish_dtm)
VALUES ('tweet014', '@thomassbright', E'\\x48657861646563696d616c20646174612069732068657821', '2023-08-04 12:00:00');

-- Searching for encoded data (Hexadecimal) in content
SELECT tweet_message_id, tweeter_account_id, content
FROM   car.tweet
WHERE  content ~ E'\\\\x[0-9A-Fa-f]+';



p6.28
\c about_x

SELECT date_trunc('hour', publish_dtm) AS tweet_hour, count(*) AS tweet_count
FROM car.tweet
GROUP BY tweet_hour
ORDER BY tweet_hour;



p6.29
\c about_x

SELECT
    COUNT(*) AS total_tweets,
    SUM(CASE WHEN image IS NOT NULL THEN 1 ELSE 0 END) AS tweets_with_images,
    SUM(CASE WHEN image IS NULL THEN 1 ELSE 0 END) AS tweets_without_images
FROM car.tweet;



p6.30
\c about_x

SELECT tweeter_account_id, COUNT(*) AS tweet_count
FROM car.tweet
GROUP BY tweeter_account_id
ORDER BY tweet_count DESC;



p6.31
--connect to database about_x
\c about_x

--set off expanded display off
\x off  

--Check existing unstructured data in car.tweet 
SELECT tweet_message_id, content FROM car.tweet;

--check existing structured data in car.product
SELECT product_name FROM car.product;

--Clear old tweet_comment 
TRUNCATE car.tweet_comment;

--Ok, let create insights in semi-structured data type by blending unstructured data
--with structured data
INSERT INTO car.tweet_comment (comment_id, comment_dtm, comment, tweet_message_id)
SELECT
    'comment_id_for_tweet_' || tweet_message_id,
     current_timestamp, -- or the desired timestamp
     JSON_BUILD_OBJECT('text', 'This tweet mentioned product: ' || product_name),
     tweet_message_id
FROM car.tweet AS tweet
JOIN car.product AS product
ON   tweet.content ILIKE '%' || product.product_name || '%';

--set on expanded display 
\x on

--get the semi-structured data
SELECT * FROM car.tweet_comment;



p6.32

\d space.space_travel_schedule
\d space.space_trip
\d car.customer
\d car.order_header

CREATE TABLE space.dw_orders AS
SELECT
    t.trip_id,
    c.customer_id,
    t.destination,
    t.departure_from,
    t.departure_dtm AS travel_departure_dtm,
    t.return_dtm AS travel_return_dtm,
    t.price AS travel_price,
    o.order_no,
    o.order_dtm AS order_date,
    o.delivery_address_1 AS delivery_address,
    o.discount_rate,
    o.order_net_total AS order_total
FROM space.space_travel_schedule t
JOIN space.space_trip s ON t.trip_id = s.trip_id
JOIN car.customer c ON s.customer_id = c.customer_id
JOIN car.order_header o ON c.customer_id = o.customer_id;

CREATE INDEX dw_orders_idx_01 ON space.dw_orders (order_no, customer_id);

SELECT * FROM space.dw_orders;

COPY (
    SELECT
        t.trip_id,
        c.customer_id,
        t.destination,
        t.departure_from,
        t.departure_dtm AS travel_departure_dtm,
        t.return_dtm AS travel_return_dtm,
        t.price AS travel_price,
        o.order_no,
        o.order_dtm AS order_date,
        o.delivery_address_1 AS delivery_address,
        o.discount_rate,
        o.order_net_total AS order_total
    FROM space.space_travel_schedule t
    JOIN space.space_trip s ON t.trip_id = s.trip_id
    JOIN car.customer c ON s.customer_id = c.customer_id
    JOIN car.order_header o ON c.customer_id = o.customer_id
) TO 'C:\Users\tony\dw_order.csv' WITH CSV HEADER;

Note: change C:\Users\tony\ to your local path



p6.33
--connect to database about_x
\c about_x

SELECT
   trip_id, destination, departure_from,
   CASE
       WHEN price::numeric >= 1000000 THEN 'Expensive'
       WHEN price::numeric >= 500000 THEN 'Moderate'
       ELSE 'Affordable'
   END AS price_category
FROM space.space_travel_schedule;

SELECT
    order_no,
    COALESCE(delivery_address_1, delivery_address_2, delivery_address_3,  delivery_address_4, 'N/A') AS delivery_address
FROM car.order_header
LIMIT 1;

SELECT
    order_no, delivery_address_1, delivery_address_2, delivery_address_3,  delivery_address_4
FROM car.order_header
LIMIT 1;



p6.34
--connect to database about_x
\c about_x

SELECT
    p.product_id,
    p.product_name,
    p.sku,
    p.origin,
    p.color,
    p.category_id,
    p.price,
    SUM(CASE WHEN od.qty IS NOT NULL THEN od.qty ELSE 0 END) AS total_qty,
    SUM(CASE WHEN od.amount IS NOT NULL THEN od.amount ELSE 0 END) AS total_amount
FROM car.product p
LEFT JOIN car.order_detail od ON p.product_id = od.product_id
GROUP BY
    p.product_id,
    p.product_name,
    p.sku,
    p.origin,
    p.color,
    p.category_id,
    p.price;

SELECT product_id, 'product_name' AS attribute, product_name AS value
FROM   car.product
UNION ALL
SELECT product_id, 'sku' AS attribute, sku AS value
FROM   car.product
UNION ALL
SELECT product_id, 'origin' AS attribute, origin AS value
FROM   car.product
UNION ALL
SELECT product_id, 'color' AS attribute, color AS value
FROM   car.product
UNION ALL
SELECT product_id, 'category_id' AS attribute, category_id AS value
FROM   car.product
UNION ALL
SELECT product_id, 'qty' AS attribute, qty::text AS value
FROM car.order_detail
WHERE qty IS NOT NULL
UNION ALL
SELECT product_id, 'amount' AS attribute, amount::text AS value
FROM car.order_detail
WHERE amount IS NOT NULL;




p7.
\c about_x

--Check the table structure
\d space.space_trip
\d car.order_header



p7.1
--Insert sample data – a new customer
INSERT INTO car.customer (
 customer_id, title, first_name, middle_name, last_name, email, phone, address_1,  address_2, address_3, address_4,city, country, postal_code, 
 tweeter_account_id)
VALUES (
 'C230000002', 'Mr.', 'David', 'M', 'Lee', 'david@davidtest.com', '+01-98765432', 
 'Unit 33, Eight Street', NULL, NULL, NULL, 'Los Angeles', 'USA', '934567', '@davidmlee');

--Insert sample data – a new space trip booking
INSERT INTO space.space_trip (trip_id, customer_id, fee, amount_paid)
VALUES ('S000000002', 'C230000002', '1,000,000.00', '1,00,000.00');

SELECT trip_id, customer_id, fee FROM space.space_trip;

SELECT order_no, customer_id, order_net_total FROM car.order_header;

--Inner Join
SELECT st.trip_id, st.fee AS trip_amount,
       c.customer_id,
       oh.order_no AS car_order_id, oh.order_net_total AS car_order_amount
FROM  space.space_trip st
INNER JOIN car.customer c ON st.customer_id = c.customer_id
INNER JOIN car.order_header oh ON c.customer_id = oh.customer_id;

--Inner join, try again 
SELECT st.trip_id, st.fee AS trip_amount,
       c.customer_id,
       oh.order_no AS car_order_id, oh.order_net_total AS car_order_amount
FROM space.space_trip st
JOIN car.customer c ON st.customer_id = c.customer_id
JOIN car.order_header oh ON c.customer_id = oh.customer_id;



p7.2
--Full Outer Join
SELECT st.trip_id, st.fee AS trip_amount,
       c.customer_id,
       oh.order_no AS car_order_id, oh.order_net_total AS car_order_amount
FROM  space.space_trip st
FULL OUTER JOIN car.customer c ON st.customer_id = c.customer_id
FULL OUTER JOIN car.order_header oh ON c.customer_id = oh.customer_id;


--Full Outer Join – improved version
SELECT 
    CASE
        WHEN st.trip_id IS NOT NULL THEN st.trip_id
        ELSE 'No space trip booked'
    END AS trip_id,
    CASE
        WHEN st.fee IS NOT NULL THEN st.fee::text
        ELSE '0'
    END AS trip_amount,
    c.customer_id,
    CASE
        WHEN oh.order_no IS NOT NULL THEN oh.order_no
        ELSE 'No car purchased'
    END AS car_order_id,
    CASE
        WHEN oh.order_net_total IS NOT NULL THEN oh.order_net_total::text
        ELSE '0'
    END AS car_order_amount
FROM  space.space_trip st
FULL OUTER JOIN car.customer c ON st.customer_id = c.customer_id
FULL OUTER JOIN car.order_header oh ON c.customer_id = oh.customer_id;



p7.3
--Left Outer Join 
SELECT 
    CASE
        WHEN st.trip_id IS NOT NULL THEN st.trip_id
        ELSE 'No space trip booked'
    END AS trip_id,
    CASE
        WHEN st.fee IS NOT NULL THEN st.fee::text
        ELSE '0'
    END AS trip_amount,
    c.customer_id,
    CASE
        WHEN oh.order_no IS NOT NULL THEN oh.order_no
        ELSE 'No car purchased'
    END AS car_order_id,
    CASE
        WHEN oh.order_net_total IS NOT NULL THEN oh.order_net_total::text
        ELSE '0'
    END AS car_order_amount
FROM  space.space_trip st
LEFT OUTER JOIN car.customer c ON st.customer_id = c.customer_id
LEFT OUTER JOIN car.order_header oh ON c.customer_id = oh.customer_id;



p7.4
--Right Outer Join 
SELECT 
    CASE
        WHEN st.trip_id IS NOT NULL THEN st.trip_id
        ELSE 'No space trip booked'
    END AS trip_id,
    CASE
        WHEN st.fee IS NOT NULL THEN st.fee::text
        ELSE '0'
    END AS trip_amount,
    c.customer_id,
    CASE
        WHEN oh.order_no IS NOT NULL THEN oh.order_no
        ELSE 'No car purchased'
    END AS car_order_id,
    CASE
        WHEN oh.order_net_total IS NOT NULL THEN oh.order_net_total::text
        ELSE '0'
    END AS car_order_amount
FROM  space.space_trip st
RIGHT OUTER JOIN car.customer c ON st.customer_id = c.customer_id
RIGHT OUTER JOIN car.order_header oh ON c.customer_id = oh.customer_id
ORDER BY c.customer_id;


WITH 
trip_amounts AS (
    SELECT    st.customer_id,
              SUM(COALESCE(st.fee::numeric, 0)) AS total_trip_amount
    FROM      space.space_trip st
    GROUP BY  st.customer_id
),
Car_order_amounts AS (
    SELECT    c.customer_id,
              SUM(COALESCE(oh.order_net_total::numeric, 0)) AS total_car_order_amount
    FROM      car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY  c.customer_id
)
SELECT
    CASE
        WHEN ta.total_trip_amount IS NOT NULL THEN ta.total_trip_amount::money
        ELSE '0'::money
    END AS total_trip_amount,
    c.customer_id,
    CASE
        WHEN coa.total_car_order_amount IS NOT NULL THEN coa.total_car_order_amount::money
        ELSE '0'::money
    END AS total_car_order_amount
FROM  car.customer c
LEFT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
LEFT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY  c.customer_id;


--Try again- use RIGHT JOIN
WITH 
trip_amounts AS (
    SELECT    st.customer_id,
              SUM(COALESCE(st.fee::numeric, 0)) AS total_trip_amount
    FROM      space.space_trip st
    GROUP BY  st.customer_id
),
Car_order_amounts AS (
    SELECT    c.customer_id,
              SUM(COALESCE(oh.order_net_total::numeric, 0)) AS total_car_order_amount
    FROM      car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY  c.customer_id
)
SELECT
    CASE
        WHEN ta.total_trip_amount IS NOT NULL THEN ta.total_trip_amount::money
        ELSE '0'::money
    END AS total_trip_amount,
    ta.customer_id,
    CASE
        WHEN coa.total_car_order_amount IS NOT NULL THEN coa.total_car_order_amount::money
        ELSE '0'::money
    END AS total_car_order_amount
FROM  car.customer c
RIGHT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
RIGHT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY  c.customer_id;



p7.5
WITH order_accumulation AS (
     SELECT
        DATE_TRUNC('day', oh.order_dtm) AS order_date,
        SUM(od.amount) AS accumulated_amount,
        SUM(od.qty) AS accumulated_qty
     FROM car.order_header oh
     JOIN car.order_detail od ON oh.order_no = od.order_no
     GROUP BY order_date
)
SELECT
     TO_CHAR(order_date, 'YYYY-MM-DD') AS date,
     SUM(accumulated_amount) OVER (ORDER BY order_date) AS accumulated_amount,
     SUM(accumulated_qty) OVER (ORDER BY order_date) AS accumulated_qty
FROM order_accumulation
ORDER BY order_date;


--Below is the order detail
SELECT oh.order_dtm, od.amount, od.qty 
FROM car.order_detail od 
JOIN car.order_header oh ON od.order_no = oh.order_no order by oh.order_dtm;



p7.6
--Understand the data - product
SELECT COUNT(1) FROM car.product;

--Understand the data – category
SELECT COUNT(1) FROM car.category;

SELECT c.category_id, c.description, p.product_id, p.product_name
FROM car.category c
CROSS JOIN car.product p;

SELECT c.category_id, c.description, p.product_id, p.product_name
FROM car.category c
FULL OUTER JOIN car.product p ON c.category_id = p.category_id;

-- Insert sample data
INSERT INTO car.category (category_id, description)
VALUES ('CT000006', 'Extra Battery');

SELECT c.category_id, c.description, p.product_id, p.product_name
FROM car.category c
FULL OUTER JOIN car.product p ON c.category_id = p.category_id;

SELECT c.category_id, c.description, p.product_id, p.product_name
FROM  car.category c
CROSS JOIN car.product p;



p7.7
SELECT cd1.category_id, cd1.designer
FROM car.category_designer cd1
INNER JOIN car.category_designer cd2 ON cd1.category_id = cd2.category_id AND 
           cd1.designer != cd2.designer;



p8.
--Sample SQL
WITH 
trip_amounts AS (
    SELECT    st.customer_id,
              SUM(COALESCE(st.fee::numeric, 0)) AS total_trip_amount
    FROM      space.space_trip st
    GROUP BY  st.customer_id
),
Car_order_amounts AS (
    SELECT    c.customer_id,
              SUM(COALESCE(oh.order_net_total::numeric, 0)) AS total_car_order_amount
    FROM      car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY  c.customer_id
)
SELECT
    CASE
        WHEN ta.total_trip_amount IS NOT NULL THEN ta.total_trip_amount::money
        ELSE '0'::money
    END AS total_trip_amount,
    c.customer_id,
    CASE
        WHEN coa.total_car_order_amount IS NOT NULL THEN coa.total_car_order_amount::money
        ELSE '0'::money
    END AS total_car_order_amount
FROM  car.customer c
LEFT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
LEFT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY  c.customer_id;



p8.1
--Analyze this query, using EXPLAIN
EXPLAIN
WITH 
trip_amounts AS (
    SELECT    st.customer_id,
              SUM(COALESCE(st.fee::numeric, 0)) AS total_trip_amount
    FROM      space.space_trip st
    GROUP BY  st.customer_id
),
Car_order_amounts AS (
    SELECT    c.customer_id,
              SUM(COALESCE(oh.order_net_total::numeric, 0)) AS total_car_order_amount
    FROM      car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY  c.customer_id
)
SELECT
    CASE
        WHEN ta.total_trip_amount IS NOT NULL THEN ta.total_trip_amount::money
        ELSE '0'::money
    END AS total_trip_amount,
    c.customer_id,
    CASE
        WHEN coa.total_car_order_amount IS NOT NULL THEN coa.total_car_order_amount::money
        ELSE '0'::money
    END AS total_car_order_amount
FROM  car.customer c
LEFT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
LEFT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY  c.customer_id;



p8.2
--Analyze this query, using EXPLAIN
EXPLAIN ANALYSE
WITH 
trip_amounts AS (
    SELECT    st.customer_id,
              SUM(COALESCE(st.fee::numeric, 0)) AS total_trip_amount
    FROM      space.space_trip st
    GROUP BY  st.customer_id
),
Car_order_amounts AS (
    SELECT    c.customer_id,
              SUM(COALESCE(oh.order_net_total::numeric, 0)) AS total_car_order_amount
    FROM      car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY  c.customer_id
)
SELECT
    CASE
        WHEN ta.total_trip_amount IS NOT NULL THEN ta.total_trip_amount::money
        ELSE '0'::money
    END AS total_trip_amount,
    c.customer_id,
    CASE
        WHEN coa.total_car_order_amount IS NOT NULL THEN coa.total_car_order_amount::money
        ELSE '0'::money
    END AS total_car_order_amount
FROM  car.customer c
LEFT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
LEFT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY  c.customer_id;



p8.3
--Query 1:
EXPLAIN ANALYSE
SELECT
COALESCE(SUM(st.fee::money), '0.00'::money) AS total_trip_amount,
c.customer_id,
COALESCE(SUM(oh.order_net_total::money), '0.00'::money) AS total_car_order_amount
FROM  car.customer c
LEFT JOIN space.space_trip st ON c.customer_id = st.customer_id
LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
GROUP BY c.customer_id
ORDER BY c.customer_id;


--Query 2:
EXPLAIN ANALYSE
WITH 
trip_amounts AS (
    SELECT st.customer_id, COALESCE(SUM(st.fee)::money, 0::money) AS total_trip_amount
    FROM space.space_trip st
    GROUP BY st.customer_id
),
car_order_amounts AS (
    SELECT c.customer_id, COALESCE(SUM(oh.order_net_total)::money, 0::money) AS total_car_order_amount
    FROM car.customer c
    LEFT JOIN car.order_header oh ON c.customer_id = oh.customer_id
    GROUP BY c.customer_id
)
SELECT  ta.total_trip_amount, c.customer_id, coa.total_car_order_amount
FROM  car.customer c
LEFT JOIN trip_amounts ta ON c.customer_id = ta.customer_id
LEFT JOIN car_order_amounts coa ON c.customer_id = coa.customer_id
ORDER BY c.customer_id;



p8.4
SELECT
    st.trip_id,
    st.customer_id,
    st.fee
FROM space.space_trip st
INNER JOIN car.customer c ON st.customer_id = c.customer_id
INNER JOIN car.order_header oh ON c.customer_id = oh.customer_id
WHERE
    oh.order_net_total > '$10000'::money  -- Pushed down to the source
    AND st.fee > '$100'::money;           -- Pushed down to the source



p8.5
--Create 1.2 million sample data in few minutes
INSERT INTO car.tweet (
    tweet_message_id, tweeter_account_id, content, publish_dtm, image, video, url)
SELECT
    md5(random()::text || clock_timestamp()::text)::CHARACTER VARYING(64) AS tweet_message_id,
    '@thomassbright' AS tweeter_account_id,
    'Sample tweet content' AS content,
    NOW() AS publish_dtm,
    null AS image,
    null AS video,
    null AS url
FROM GENERATE_SERIES (1, 1200000);

-- Enable parallel query and increase the number of parallel workers, and analyze it
SET max_parallel_workers = 4;  -- Adjust the number as needed
SET max_parallel_workers_per_gather = 4;  -- Adjust the number as needed

EXPLAIN
SELECT tweet_message_id, tweeter_account_id
FROM car.tweet
WHERE publish_dtm >= '2023-01-01'::timestamp
ORDER BY publish_dtm;

--Drop an index to see the execution plan without index
DROP INDEX car.tweet_idx_02;

--Try again
SET max_parallel_workers = 4;  -- Adjust the number as needed
SET max_parallel_workers_per_gather = 4;  -- Adjust the number as needed

EXPLAIN ANALYSE
SELECT tweet_message_id, tweeter_account_id
FROM car.tweet
WHERE publish_dtm >= '2023-09-10 15:25:46.329222'::timestamp
ORDER BY publish_dtm;

--Rebuild the index to see the execution plan improved
CREATE INDEX CONCURRENTLY tweet_idx_02 ON car.tweet (publish_dtm, tweet_message_id, tweeter_account_id);

SET max_parallel_workers = 4;  -- Adjust the number as needed
SET max_parallel_workers_per_gather = 4;  -- Adjust the number as needed

EXPLAIN ANALYSE
SELECT tweet_message_id, tweeter_account_id
FROM car.tweet
WHERE publish_dtm >= '2023-09-10 15:25:46.329222'::timestamp
ORDER BY publish_dtm;



p8.6
-- Create a materialized view to store the total order amount for each customer
CREATE MATERIALIZED VIEW customer_total_order_amount AS
SELECT c.customer_id, SUM(oh.order_net_total::numeric) AS total_order_amount
FROM car.customer c
JOIN car.order_header oh ON c.customer_id = oh.customer_id
GROUP BY c.customer_id;

-- Refresh the materialized view to update its data (you can schedule this as needed)
REFRESH MATERIALIZED VIEW customer_total_order_amount;

-- Query the materialized view to get total order amounts for customers
SELECT * FROM customer_total_order_amount;



p8.7
-- Using IN subquery to find customers who have placed orders
SELECT c.customer_id, c.first_name, c.last_name
FROM car.customer c
WHERE c.customer_id IN (
    SELECT oh.customer_id
    FROM car.order_header oh
);

-- Using EXISTS subquery to find customers who have placed orders
SELECT c.customer_id, c.first_name, c.last_name
FROM car.customer c
WHERE EXISTS (
    SELECT 1
    FROM car.order_header oh
    WHERE oh.customer_id = c.customer_id
);



p8.8
\d car.tweet

--How to reindex all indexes of a table.  Note: This will lock the table
REINDEX TABLE car.tweet;

--Reindex a specific index and use CONCURRENTLY.  Note: This will NOT lock the table
REINDEX INDEX CONCURRENTLY car.tweet_idx_02;



p8.9
(session 1)
\c about_x

-- Start Transaction A
BEGIN;

-- Attempt to update customer C00000001
UPDATE car.customer
SET first_name = 'NewFirstNameA'
WHERE customer_id = 'C00000001';

-- Pause Transaction A (do not commit)


(seesion 2)
\c about_x

-- Start Transaction B
BEGIN;

-- Attempt to update customer C00000002
UPDATE car.customer
SET first_name = 'NewFirstNameB'
WHERE customer_id = 'C00000002';

-- Pause Transaction B (do not commit)


(seesion 3)
\c about_x

--Deadlock Detection
SELECT blocked.query AS blocked_query, waiting.query AS blocking_query
FROM pg_stat_activity AS blocked
JOIN pg_stat_activity AS waiting ON waiting.pid = blocked.pid
WHERE blocked.query <> '<IDLE>' AND waiting.query <> '<IDLE>';


(session 1)
ROLLBACK;

(session 2) 
ROLLBACK;

(seesion 3)
\c about_x
--Deadlock Detection
SELECT blocked.query AS blocked_query, waiting.query AS blocking_query
FROM pg_stat_activity AS blocked
JOIN pg_stat_activity AS waiting ON waiting.pid = blocked.pid
WHERE blocked.query <> '<IDLE>' AND waiting.query <> '<IDLE>';



p.9
(Please refer to the book)



p10.
\c about_x
--Configure the data masking
CREATE EXTENSION IF NOT EXISTS anon CASCADE;
  
NOTICE:  installing required extension "pgcrypto"
CREATE EXTENSION

--Start data masking extension
SELECT anon.start_dynamic_masking();  

--Create a test account (a role) named test01 who can only get the masked data
CREATE ROLE test01 LOGIN;

--apply the masking to test01
SECURITY LABEL FOR anon ON ROLE test01 IS 'MASKED'; 

--Create a sample table
CREATE TABLE info ( name varchar(30), passport_id varchar(15) );

--Insert 2 sample records into the table
INSERT INTO info VALUES ('Mr. Andrew Big ', 'A123456(1)');
INSERT INTO info VALUES ('Miss Beautiful White', 'B234567(2)');

SELECT name, passport_id FROM info;

--Set masking
SECURITY LABEL FOR anon ON COLUMN info.passport_id IS 'MASKED WITH FUNCTION anon.partial(passport_id,5,$$***$$,0)';

--Login psql as user: test01, from command prompt of Linux
psql -U test01 

--Select the records using standard SELECT SQL
SELECT name, passport_id FROM info;


psql -U postgres
--To unmask the secure label for a role:
SECURITY LABEL FOR anon ON ROLE test01 IS NULL;

--To disable the mask:
SELECT anon.stop_dynamic_masking();



p10.1
--Connect to your database
\c about_x

SELECT customer_id, city 
FROM car.customer 
WHERE customer_id = '105' OR 1=1;



p10.2
PREPARE safe_query (text) AS
SELECT  customer_id, city
FROM    car.customer
WHERE   customer_id = $1;
--Execute the prepared statement with user input
EXECUTE safe_query('105');

EXECUTE safe_query('105 OR 1=1');
EXECUTE safe_query('1=1');
EXECUTE safe_query('C00000001');

DEALLOCATE safe_query;



p10.3
\c about_x

--Enable pgcrypto extension in database of about_x
CREATE EXTENSION pgcrypto;

--Drop the column if it exists
ALTER TABLE car.customer DROP COLUMN IF EXISTS social_security_no;

--Add the column as bytea
ALTER TABLE car.customer ADD COLUMN social_security_no BYTEA;

\d car.customer

UPDATE car.customer
SET social_security_no =  ENCODE(DIGEST('11111111111'::TEXT, 'sha256'::TEXT), 'HEX'::TEXT)::BYTEA
WHERE customer_id = 'C230000003';

SELECT social_security_no FROM car.customer WHERE customer_id = 'C230000003';

SELECT customer_id, social_security_no
FROM  car.customer 
WHERE social_security_no = 
      ENCODE(DIGEST('11111111111'::TEXT, 'sha256'::TEXT), 'HEX'::TEXT)::BYTEA;


UPDATE car.customer
SET social_security_no = HMAC('222222222'::BYTEA, 'MY_SECRET_KEY'::BYTEA, 'sha256')
WHERE customer_id = 'C230000002';

SELECT customer_id, social_security_no 
FROM car.customer
WHERE customer_id = 'C230000002';

SELECT customer_id, social_security_no
FROM  car.customer 
WHERE social_security_no = HMAC('222222222'::BYTEA, 'MY_SECRET_KEY'::BYTEA, 'sha256');



p10.4
--Connect to your database
\c about_x

--Enable pgcrypto extension in database of about_x
CREATE EXTENSION pgcrypto;

UPDATE car.customer
SET social_security_no = PGP_SYM_ENCRYPT('333333333', 'MY_SECRET_KEY')
WHERE customer_id = 'C230000001';

SELECT customer_id, social_security_no 
FROM car.customer
WHERE customer_id = 'C230000001';

-- Decrypt the data
SELECT customer_id, 
       PGP_SYM_DECRYPT(social_security_no, 'MY_SECRET_KEY') as social_security_no
FROM car.customer
WHERE customer_id = 'C230000001';



p10.5
(please refer to the book)



p10.6
--Connect to your database
\c about_x

--Enable pgcrypto extension in database of about_x
CREATE EXTENSION pgcrypto;

--Create a new sample record to car.customer
INSERT INTO car.customer (
 customer_id, title, first_name, middle_name, last_name,
 email, phone,  
 address_1, address_2, address_3, address_4,
 city, country, postal_code, 
 tweeter_account_id)
VALUES (
 'C230000004', 'Mr.', 'Peter', '', 'Pan',
 'peter@test.org', '+01-23456789', 
 'Unit 1, Sixth Street', NULL, NULL, NULL,
 'Los Angeles', 'USA', '9345678',
 '@petertest');


--Store the Social Security Number which is encrypted 
UPDATE car.customer
SET social_security_no = 
 PGP_PUB_ENCRYPT('444444444', DEARMOR('

-----BEGIN PGP PUBLIC KEY BLOCK-----

( YOUR PUBLIC HERE )

-----END PGP PUBLIC KEY BLOCK-----
'))
WHERE customer_id = 'C230000004';


SELECT customer_id, social_security_no
FROM car.customer 
WHERE customer_id = 'C230000004';


--Decrypt the value if you have the decryption key
SELECT customer_id, CONVERT_FROM(
    PGP_PUB_DECRYPT_BYTEA (social_security_no, DEARMOR('

-----BEGIN PGP PRIVATE KEY BLOCK-----

(YPUR KEY HERE)


-----END PGP PRIVATE KEY BLOCK-----

')),'UTF8') AS decrypted_social_security_no
FROM  car.customer
WHERE customer_id = 'C230000004';


### END ### 
