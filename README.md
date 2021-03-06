# MySQL In Action
---


## Activation 
``` 
gitpod /workspace/mysql-in-action $ mysql
```

### Retrieving Chinook Database SQL Script File
```
gitpod /workspace/mysql-in-action $ wget https://raw.githubusercontent.com/lerocha/chinook-database/master/ChinookDatabase/DataSources/Chinook_MySql_AutoIncrementPKs.sql
```

Using the -v switch becuase this command can take upto 5 minutes to complete. -v for verbose, this outputs what's going.
```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| Chinook            |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)
```

### Accessing/testing database Chinook and running a simple script
```
mysql> use Chinook;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+-------------------+
| Tables_in_Chinook |
+-------------------+
| Album             |
| Artist            |
| Customer          |
| Employee          |
| Genre             |
| Invoice           |
| InvoiceLine       |
| MediaType         |
| Playlist          |
| PlaylistTrack     |
| Track             |
+-------------------+
11 rows in set (0.00 sec)

mysql> desc Genre;
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| GenreId | int          | NO   | PRI | NULL    | auto_increment |
| Name    | varchar(120) | YES  |     | NULL    |                |
+---------+--------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> tee mysql-file.txt
Logging to file 'mysql-file.txt'

mysql> notee
Outfile disabled.
mysql> source test.sql
+----------+
| count(*) |
+----------+
|     3503 |
+----------+
1 row in set (0.00 sec)

+----------+
| count(*) |
+----------+
|      275 |
+----------+
1 row in set (0.00 sec)

mysql> 
```

### Using the JOIN keyword to select data from multiple tables
```
mysql> select * from Album limit 5;
+---------+---------------------------------------+----------+
| AlbumId | Title                                 | ArtistId |
+---------+---------------------------------------+----------+
|       1 | For Those About To Rock We Salute You |        1 |
|       2 | Balls to the Wall                     |        2 |
|       3 | Restless and Wild                     |        2 |
|       4 | Let There Be Rock                     |        1 |
|       5 | Big Ones                              |        3 |
+---------+---------------------------------------+----------+
5 rows in set (0.00 sec)

mysql> select Title, Name from Album
    -> join Artist on Album.ArtistId = Artist.ArtistId
    -> limit 5;
+---------------------------------------+-----------+
| Title                                 | Name      |
+---------------------------------------+-----------+
| For Those About To Rock We Salute You | AC/DC     |
| Balls to the Wall                     | Accept    |
| Restless and Wild                     | Accept    |
| Let There Be Rock                     | AC/DC     |
| Big Ones                              | Aerosmith |
+---------------------------------------+-----------+
5 rows in set (0.01 sec)

mysql> 
```

### Basic CRUD operations
```
mysql> desc Genre;
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| GenreId | int          | NO   | PRI | NULL    | auto_increment |
| Name    | varchar(120) | YES  |     | NULL    |                |
+---------+--------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> insert into Genre (Name) values ('Trad');
Query OK, 1 row affected (0.07 sec)

mysql> select last_insert_ID();
+------------------+
| last_insert_ID() |
+------------------+
|               26 |
+------------------+
1 row in set (0.00 sec)

mysql> select Name from Genre where GenreId = 26;
+------+
| Name |
+------+
| Trad |
+------+
1 row in set (0.00 sec)

mysql> update Genre  set Name = 'Traditional' where Name = 'Trad';
Query OK, 1 row affected (0.07 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select Name from Genre where GenreId = 26;
+-------------+
| Name        |
+-------------+
| Traditional |
+-------------+
1 row in set (0.00 sec)

mysql> delete from Genre where Name = 'Traditional';
Query OK, 1 row affected (0.05 sec)

mysql> select Name from Genre where GenreId = 26;
Empty set (0.00 sec)
```