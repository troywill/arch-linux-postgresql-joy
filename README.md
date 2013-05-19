<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Inspect the PostgreSQL environment</a></li>
<li><a href="#sec-2">2. How to create users</a>
<ul>
<li><a href="#sec-2-1">2.1. Creating new users with SQL from PostgreSQL interactive terminal</a></li>
<li><a href="#sec-2-2">2.2. Creating new uses with the createuser program</a>
<ul>
<li><a href="#sec-2-2-1">2.2.1. Create the user joe as a superuser, and assign a password immediately</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#sec-3">3. Creating new databases</a>
<ul>
<li><a href="#sec-3-1">3.1. Creating a new database with SQL from PostgreSQL interactive terminal</a></li>
</ul>
</li>
<li><a href="#sec-4">4. Create and Delete databases</a>
<ul>
<li><a href="#sec-4-1">4.1. Create a database</a></li>
</ul>
</li>
<li><a href="#sec-5">5. Documentation Links</a>
<ul>
<li><a href="#sec-5-1">5.1. PostgreSQL: Documentation www.postgresql.org/docs/</a></li>
</ul>
</li>
</ul>
</div>
</div>
# Inspect the PostgreSQL environment

-   Become the postgres user
    
        sudo su - postgres

-   psql commands help
    
        \?

-   List the users
    
        \dg

-   List all the databases
    
        \l

# How to create users

## Creating new users with SQL from PostgreSQL interactive terminal

1.  [X] Become the "postgres" user
    
        sudo su - postgres

2.  [X] Open the PostgreSQL interactive terminal
    
        psql

## Creating new uses with the createuser program

### Create the user joe as a superuser, and assign a password immediately

1.  [ ] Become the postgres user
    
        sudo su - postgres

2.  Run createuser with  
    
        $ createuser --pwprompt --superuser --echo joe
        Enter password for new role: xyzzy
        Enter it again: xyzzy
        CREATE ROLE joe PASSWORD 'md5b5f5ba1a423792b526f799ae4eb3d59e' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;

# Creating new databases

## Creating a new database with SQL from PostgreSQL interactive terminal

1.  Become the postgres user
    
        sudo su - postgres

2.  Run the "[CREATE USER](http://www.postgresql.org/docs/current/static/sql-createdatabase.html)" SQL command
    
        CREATE

# Create and Delete databases

## Create a database

# Documentation Links

## [PostgreSQL: Documentation](http://www.postgresql.org/docs/) www.postgresql.org/docs/

-   [Current Manual](http://www.postgresql.org/docs/manuals/)
