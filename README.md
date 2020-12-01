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