## psql comand line
[psql documentation](https://www.postgresql.org/docs/current/app-psql.html)  
psql -> connect through bash  
\l -> list databases  
\c (database name) -> connect to db  
\dt -> list tables in database *requires connection to DB  
**after connecting to db you can execute SQL, each statement must end with ';'**  
\q -> quit psql  
  
psql -U username -d mydatabase -c 'SELECT * FROM mytable'