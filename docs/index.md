# Welcome to ContestBase

This app serves to document the stances, actions, policies, and communications of lawmakers and candidate lawmakers. The idea is that any organizer or group of organizers should be able to track these relationships and to follow the state of the political arena if they are seeking to leverage state power or the political stage to further or to advertise their political agenda to gain followers or win material gains for working people in a greater strategy to win power for the working class.

## Contest Base Concepts

* `Office` - This is a seat that a legislator holds in a body, or other elected position. These have a corresponding region they represent.
* `Candidate` - Legislators.
* `Contest` - Either a primary, general, or special election in a given year with (hopefully) many candidates for an office.
* `Maps` - Maps are supposed to represent.

## Getting Started

A key motivator for developing this tool was not only the desire to have a robust interface, but to own the data. As such, this is a self-hosted website running on Node.js and MySQL (future support for other databases?).

    $ node -v
    v8.16.0
    $ mysqld -V
    mysqld  Ver 5.7.26-0ubuntu0.18.04.1 for Linux on x86_64 ((Ubuntu))

Generally the steps necessary to get a new instance running are:

1. Creating the database, a user and password with all privileges on this database.
1. Installing the schema and adding the first user from the command line
1. Editing the configuration file
1. (Recommended) Configuring a reverse proxy/SSL
1. (Recommended) Writing a startup service script (`Upstart`, `systemd`, etc)

### Creating the database

For MySQL databases, the following commands should work for creating a database for use with Contest Base:

    $ mysql -uroot -p
    Enter password: 
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 5
    Server version: 5.7.26-0ubuntu0.18.04.1 (Ubuntu)

    Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    mysql> create database contestbasedb;
    Query OK, 1 row affected (0.00 sec)

    mysql> create user 'cbuser'@'localhost' identified by 'cbuserpwd';
    Query OK, 0 rows affected (0.00 sec)

    mysql> grant all on contestbasedb.* to 'cbuser'@'localhost' with grant option;
    Query OK, 0 rows affected (0.00 sec)

    mysql> flush privileges;
    Query OK, 0 rows affected (0.00 sec)

    mysql> ^DBye

### Installing the schema

    $ pwd
    /path/to/source/code
    $ bin/contestbase-cli database wipe
    $ bin/contestbase-cli user add user@example.com password

### Finish editing the configuration

See Configuration docs for more information, and then simply:

    $ $(which yarn || which npm) start
