### postgres_QL

### Notes
- master password hint: the 3rd and 4th 5 letter words
- you have a master password and a database password


### installation

- `sudo apt-get install postgresql`
- default user: postgres
- `sudo service postgresql status` for checking the status of the database
- `sudo service postgresql start` to start running your database
- `sudo service postgresql stop` to stop running your database.
- `sudo passwd postgres` to set the password
- `sudo -u postgres psql` connect to postgres service

#### for windows
- install `PostgreSQL server`
- for frontend install `pgAdmin4`
- for installing additional packages install `Stack Builder`
- command line tools
- set everything to defaults
- add `C:\Program Files\PostgreSQL\15\bin` to environment variables

### connecting to a server
- use SQL shell
- server = localhost
- Database = [database-name]
- Port = 5432
- and use `username` and `password`

#### commands
- `SELECT version();`
- `SELECT now();`
- `CREATE DATABASE [database-name];
- `\l`
- `\c [database-name]`
- eg.
```sql
CREATE DATABASE colors (ColorID int, ColorName char(20));
INSERT INTO colors VALUES (1, 'red'), (2, 'blue'), (3, 'green');
SELECT * FROM colors;
```
