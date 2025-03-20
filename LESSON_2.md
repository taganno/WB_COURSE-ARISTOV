First Terminal
```
postgres=# BEGIN;
CREATE TABLE persons(id serial, first_name text, second_name text);
INSERT INTO persons(first_name, second_name) VALUES ('vasya',
'pupkin');
INSERT INTO persons(first_name, second_name) VALUES ('fedor', 'sumkin');
COMMIT;
BEGIN
CREATE TABLE
INSERT 0 1
INSERT 0 1
COMMIT
postgres=# show transaction isolation level;
 transaction_isolation 
-----------------------
 read committed
(1 строка)

postgres=# BEGIN;
BEGIN
postgres=*# INSERT INTO persons(first_name, second_name) VALUES ('elena',
'koroleva');
INSERT 0 1
postgres=*# SELECT * FROM persons;
 id | first_name | second_name 
----+------------+-------------
  1 | vasya      | pupkin
  2 | fedor      | sumkin
  3 | elena      | koroleva
(3 строки)

postgres=*# commit;
COMMIT
postgres=# BEGIN transaction isolation level repeatable read;
BEGIN
postgres=*# INSERT INTO persons(first_name, second_name) VALUES ('polina',
'tsvetkova');
INSERT 0 1
postgres=*# COMMIT;
COMMIT
postgres=# 
```

Second Terminal
```
postgres=# BEGIN;
BEGIN
postgres=*# SELECT * FROM persons;
 id | first_name | second_name 
----+------------+-------------
  1 | vasya      | pupkin
  2 | fedor      | sumkin
(2 строки)

postgres=*# SELECT * FROM persons;
 id | first_name | second_name 
----+------------+-------------
  1 | vasya      | pupkin
  2 | fedor      | sumkin
  3 | elena      | koroleva
(3 строки)

postgres=*# COMMIT;
COMMIT
postgres=# BEGIN transaction isolation level repeatable read;
BEGIN
postgres=*# SELECT * FROM persons;
 id | first_name | second_name 
----+------------+-------------
  1 | vasya      | pupkin
  2 | fedor      | sumkin
  3 | elena      | koroleva
(3 строки)

postgres=*# COMMIT;
COMMIT
postgres=# SELECT * FROM persons;
 id | first_name | second_name 
----+------------+-------------
  1 | vasya      | pupkin
  2 | fedor      | sumkin
  3 | elena      | koroleva
  4 | polina     | tsvetkova
(4 строки)
```
