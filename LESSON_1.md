 wget https://storage.googleapis.com/thaibus/thai_small.tar.gz && tar -xf thai_small.tar.gz && psql < thai.sql >  <!-- Downoload DB from repository -->

```\c thai``` - Connect to DB "thai"

```\dt book.*``` - Getting the "books" schema relationships

```
select count(*) from book.ride;
 count  
--------
 144000
(1 строка)
```
Getting a list of rides from the "ride" table
