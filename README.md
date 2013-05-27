<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Inspect the PostgreSQL environment</a></li>
<li><a href="#sec-2">2. How to create users</a>
<ul>
<li><a href="#sec-2-1">2.1. Create a superuser with your login name (app-createuser.html)</a></li>
<li><a href="#sec-2-2">2.2. Creating new users with the create user client program</a>
<ul>
<li><a href="#sec-2-2-1">2.2.1. Create the user joe as a superuser, and assign a password immediately</a></li>
</ul>
</li>
<li><a href="#sec-2-3">2.3. Creating new users with CREATE USER from PostgreSQL interactive terminal</a></li>
</ul>
</li>
<li><a href="#sec-3">3. How to remove users</a>
<ul>
<li><a href="#sec-3-1">3.1. Removing users with SQL from PostgreSQL interactive terminal</a></li>
</ul>
</li>
<li><a href="#sec-4">4. How to update users </a></li>
<li><a href="#sec-5">5. Creating new databases</a>
<ul>
<li><a href="#sec-5-1">5.1. Create a new database with createdb</a></li>
<li><a href="#sec-5-2">5.2. Create a new database with createdb</a></li>
</ul>
</li>
<li><a href="#sec-6">6. How to restart PostgreSQL</a>
<ul>
<li><a href="#sec-6-1">6.1. Ubuntu</a></li>
</ul>
</li>
<li><a href="#sec-7">7. Documentation Links</a>
<ul>
<li><a href="#sec-7-1">7.1. PostgreSQL: Documentation www.postgresql.org/docs/</a></li>
</ul>
</li>
<li><a href="#sec-8">8. Heroku PostgreSQL</a></li>
<li><a href="#sec-9">9. Ubuntu Unicode encoding = 'UTF8';</a></li>
</ul>
</div>
</div>
# Inspect the PostgreSQL environment

1.  Become the postgres user
    
        $ sudo su - postgres

2.  Open the PostgreSQL interactive terminal
    
        $ psql

3.  Get help with psql commands
    
        \?

4.  List the users
    
        \dg

5.  List all the databases
    
        \l

# How to create users

## Create a superuser with your login name ([app-createuser.html](http://www.postgresql.org/docs/current/static/app-createuser.html))

    sudo -u postgres createuser --pwprompt --superuser joe

## Creating new users with the [create user](http://www.postgresql.org/docs/current/static/app-createuser.html) client program

### Create the user joe as a superuser, and assign a password immediately

1.  [X] Run the create user program
    
        createuser --pwprompt --superuser --echo joe
        Enter password for new role: xyzzy
        Enter it again: xyzzy
        CREATE ROLE joe PASSWORD 'md5b5f5ba1a423792b526f799ae4eb3d59e' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;

## Creating new users with [CREATE USER](http://www.postgresql.org/docs/current/static/sql-createdatabase.html) from PostgreSQL interactive terminal

1.  [X] Become the "postgres" user
    
        sudo su - postgres

2.  [X] Open the PostgreSQL interactive terminal
    
        psql

3.  [ ] Run the [CREATE USER](http://www.postgresql.org/docs/current/static/sql-createdatabase.html) SQL command
    
        CREATE ROLE jonathan LOGIN;

# How to remove users

## Removing users with SQL from PostgreSQL interactive terminal

1.  [ ] Become the "postgres" user
    
        $ sudo su - postgres

2.  [ ] Open the PostgreSQL interactive terminal
    
        $ psql

3.  [ ] [DROP USER](http://www.postgresql.org/docs/current/static/sql-dropuser.html)
    
        DROP USER IF EXISTS joe

# How to update users <http://www.postgresql.org/docs/current/static/sql-alteruser.html>

    ALTER USER david WITH PASSWORD 'hu8jmn3';
    ALTER USER weight WITH PASSWORD 'weight';

# Creating new databases

## Create a new database with [createdb](http://www.postgresql.org/docs/current/static/app-createdb.html)

1.  Run creatdb
    
        createdb demo --owner railsapp

## Create a new database with [createdb](http://www.postgresql.org/docs/current/static/app-createdb.html)

1.  Become the postgres user
    
        sudo su - postgres

2.  Run the "CREATE DATABASE" SQL command
    
        CREATE DATABASE sales OWNER salesapp TABLESPACE salesspace;
        CREATE DATABASE bootstrap_development OWNER bootstrap;
        CREATE DATABASE bootstrap_test OWNER bootstrap;
        CREATE DATABASE bootstrap_production OWNER bootstrap;

# How to restart PostgreSQL

## Ubuntu

    service --status-all
    sudo service postgresql-8.4  --full-restart

# Documentation Links

## [PostgreSQL: Documentation](http://www.postgresql.org/docs/) www.postgresql.org/docs/

-   [Current Manual](http://www.postgresql.org/docs/manuals/)

# Heroku PostgreSQL

# Ubuntu Unicode encoding = 'UTF8';

-   See <http://jacobian.org/writing/pg-encoding-ubuntu/>

-   See <http://blog.lnx.cx/tag/locales-fix-slicehost-ubuntu/>

In order to connect to template0, we need to change that flag:

    template1=# UPDATE pg_database SET datallowconn = TRUE
    template1-# WHERE datname = 'template0';
    UPDATE 1

Now we can connect, and drop the Template1 database in order to
replace it with a copy of Template0.

    template0=# UPDATE pg_database SET datistemplate = FALSE
    template0-# WHERE datname = 'template1';
    UPDATE 1
    
    # Risky!!! Backup First!!!
    template0=# drop database template1;
    DROP
    template0=# create database template1 with template = template0;
    create database template1 with template = template0 encoding = 'UTF8';
    CREATE
