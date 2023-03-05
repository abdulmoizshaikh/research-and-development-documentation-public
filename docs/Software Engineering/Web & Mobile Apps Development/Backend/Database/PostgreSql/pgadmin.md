# PgAdmin

## command to format code in pgadmin

solution:

```bash showLineNumbers
CTRL + SHIFT + K

OR

You can use command + Shift + k for SQL code format or beautify.
```

https://stackoverflow.com/questions/44345266/is-it-possible-to-autoformat-beautify-sql-queries-using-pgadmin4#:~:text=You%20can%20use%20command%20%2B%20Shift,SQL%20code%20format%20or%20beautify.

**PostgreSQL backup and restore database with Pgadmin4**

create backup of data in pgadmin

https://www.youtube.com/watch?v=S108Rh6XxPs&ab_channel=Learning

## If database is not deleting from pdagmin

kill-a-postgresql-session-connection

try restarting the pdadmin server using this command and delete the db it will work

```sql showLineNumbers
sudo service postgresql restart
```

https://stackoverflow.com/questions/5108876/kill-a-postgresql-session-connection

## how to truncate complete database in pdamin (remove all data from all tables of database)

> **Truncating all tables in a Postgres database**

you can do by runing this query it will create function

FrustratedWithFormsDesigner is correct, PL/pgSQL can do this. Here's the script:

```sql showLineNumbers

CREATE OR REPLACE FUNCTION truncate_tables(username IN VARCHAR) RETURNS void AS $$
DECLARE
    statements CURSOR FOR
        SELECT tablename FROM pg_tables
        WHERE tableowner = username AND schemaname = 'public';
BEGIN
    FOR stmt IN statements LOOP
        EXECUTE 'TRUNCATE TABLE ' || quote_ident(stmt.tablename) || ' CASCADE;';
    END LOOP;
END;
$$ LANGUAGE plpgsql;

```

and them just run this query

This creates a stored function (you need to do this just once) which you can afterwards use like this:

```sql showLineNumbers
$ SELECT truncate_tables('MYUSER');
// here MYUSER is your db user in mycase it was postgres
$ SELECT truncate_tables('postgres');

```

https://stackoverflow.com/questions/2829158/truncating-all-tables-in-a-postgres-database

## short key to `view data` of any table in pgadmin

just click on any table side bar (active highligh table) and then run this command to view its all data in output result

```sql showLineNumbers
Shift+Alt+v    // View data
```

https://www.pgadmin.org/docs/pgadmin4/6.18/keyboard_shortcuts.html
