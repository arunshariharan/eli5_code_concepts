---
layout: post
title:  "SQL insert statement"
date:   2021-09-16 23:04:47 +1000
categories: [sql]
tags: [sql, insert, insert into, sql server, mssql]
---

SQL statements are one of those things that I have at the tip of my tongue (or brain) but can never get them right the first go! So I am going to just write down the syntaxes, examples and some variations of SQL statements that I usually work with. To start with, lets look at `insert` statement in `SQL Server`

## UserHobbies table

Let's say I have the following table named `UserHobbies` where the datatype of `UserId` is `UNIQUEIDENTIFIER` while the other columns are `varchar(150)`

| UserId                               | HobbyType | HobbyDescription    |
| :----------------------------------- | :-------- | :------------------ |
| 0836688e-08b8-4396-af38-7756d3d7bb63 | Read Book | Harry Potter Series |

I want to insert a new row of data. So how would I go about it? 

 
## **Option 1 - Insert into ALL columns of a table**

*Syntax*
```sql
insert into <table_name>
values (col_1_value, col_2_value, ...)
```
*Example*
```sql
insert into UserHobbies
values ('92a96667-14d2-4e29-9260-838a905ed5ab', 'Sports', 'Play cricket on weekends')
```

&nbsp;&nbsp;  

This would result in the `UserHobbies` table to have the following data:

| UserId                               | HobbyType | HobbyDescription         |
| :----------------------------------- | :-------- | :----------------------- |
| 0836688e-08b8-4396-af38-7756d3d7bb63 | Read Book | Harry Potter Series      |
| 92a96667-14d2-4e29-9260-838a905ed5ab | Sports    | Play cricket on weekends |

&nbsp;&nbsp;  

It is all well and good when you have data for all the columns! But what if you did not have some information when you insert into the table?
If the column does not require a value to be present, I could just add `null` to that respective value as follows:

```sql
insert into UserHobbies
values ('29b24989-66b9-4b0f-9521-a0c495af1d2d', null ,'Does not have a hobby')
```

| UserId                               | HobbyType | HobbyDescription         |
| :----------------------------------- | :-------- | :----------------------- |
| 0836688e-08b8-4396-af38-7756d3d7bb63 | Read Book | Harry Potter Series      |
| 92a96667-14d2-4e29-9260-838a905ed5ab | Sports    | Play cricket on weekends |
| 29b24989-66b9-4b0f-9521-a0c495af1d2d | NULL      | Does not have a hobby    |


&nbsp;&nbsp;  

## **Option 2- Insert into select columns of a table**

Sometime you might have a table that auto-increments the `id` or calculates value for a particular column automatically.  
Or you might find that certain columns take `null` value and you may not need to provide values for all the columns.  
In such cases, you could try insert data into select few columns only as follows:

*Syntax*
```sql
insert into <table_name> (col_1_name, col_2_name)
values (col_1_value, col_2_value)
```

*Example*
```sql
insert into UserHobbies (UserId, HobbyType)
values ('c7f79983-9310-4a5c-9a8d-40b24e13e4b0', 'Sleep')
```

&nbsp; &nbsp;  

Executing the above would result in the following table:


| UserId                               | HobbyType | HobbyDescription         |
| :----------------------------------- | :-------- | :----------------------- |
| 0836688e-08b8-4396-af38-7756d3d7bb63 | Read Book | Harry Potter Series      |
| 92a96667-14d2-4e29-9260-838a905ed5ab | Sports    | Play cricket on weekends |
| 29b24989-66b9-4b0f-9521-a0c495af1d2d | NULL      | Does not have a hobby    |
| c7f79983-9310-4a5c-9a8d-40b24e13e4b0 | Sleep     | NULL                     |

&nbsp; &nbsp;  

**Note:**  
Even though the `UserId` is `UNIQUEIDENTIFIER`, when we do an insert, we wrap it around quotes as a string. Internally MSSQL tries to convert the string into a uniqueidentifier. If you provided an invalid GUID, it will throw a conversion error such as `Conversion failed when converting from a character string to uniqueidentifier.`

