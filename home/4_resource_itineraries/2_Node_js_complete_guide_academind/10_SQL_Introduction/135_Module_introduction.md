# 135. Module introduction
Created Tuesday 21 March 2023 at 12:29 am

## Situation
Right now, we are storing data in files.


## Problem(s)
Storing data in files is not efficient:
1. Reading and writing to files, especially larger ones is very inefficient.
2. Performing minute read, writes - i.e. "joins", "search" is slow in files. Not per se, but atleast in the way we are doing. We need some efficient data structures that are efficient for these operations.
3. There's no high level language to interact with data, we always have to write code from scratch. This also decreases the scope for optimizing interactions with the data.
4. It's difficult to have authorization levels if data is stored across files. (FIXME: really?)


## Solution (database)
The proper way to save application data, atleast if it's a significant amount, is to store it in a "database".

Physically, a database is a data stored in files and a program that manages the files (and therefore the data).

Generally, the term "database" refers to software that can manages data for us, on our computer.

Databases are good because:
1. It uses optimal data structures to store data.
2. It uses optimal algorithms to manage/manipulate data.
3. USP - supports a high level language to interact with the data. e.g. SQL (Structured Query Language)

In short databases are a systematic and fast way to work with persistent data. They're also quite convenient - because they have much of the functionality built-in and a lot of them exist already.

Note: optimality depends on the use case, amount of data, type of data and other requirements of the application.


## In this module
- SQL, NoSQL - We'll have a high-level view of two different kind of databases - Relational (aka *SQL*) databases and non-relational (aka *NoSQL*) databases
- Learn SQL
- Choosing a database - discuss how to decide what kind of database to use