# Data Definition Language (DDL) Notes Repository

Welcome to my MySQL notes repository! This section covers various aspects of MySQL, including database creation, table creation, and some useful shortcuts.

## Create Database

### Way 1:
```sql
CREATE DATABASE [database_name];    -- SHOW ERROR IF DATABASE EXISTS
```
### Way 2:
```sql
CREATE DATABASE IF NOT EXISTS [database_name];   -- NO ERROR IF DATABASE EXISTS
```


## Delete Database

### Way 1:
```sql
DROP DATABASE [database_name];    -- SHOW ERROR
```
### Way 2:
```sql
DROP DATABASE IF EXISTS [database_name];   -- NO ERROR IF DATABASE EXISTS
```


## Create Table

### Way 1:
```sql
CREATE TABLE [table_name](

   column_name   datatype_name    [NOT NULL] [DEFAULT def_value] [AUTO_INCREMENT],
   column_name   datatype_name    [NOT NULL] [DEFAULT def_value] [AUTO_INCREMENT],
   ...
   ...
   coll_Name   datatype_name     [PRIMARY KEY] [UNIQUE]  [NOT NULL] [DEFAULT def_Value] [AUTO_INCREMENT],

   CONSTRAINT  constrain_name  PRIMARY KEY(coll_Name, coll_Name_2),   -- No Space btwn ->  KEY()
                                                                      -- Declare primary key side to the datatype name is a bad practice
   CONSTRAINT  constrain_name  UNIQUE(coll_Name_3, coll_Name_4),      

   CONSTRAINT  constrain_name  FOREIGN KEY(coll_Name_5, coll_Name_6)
                               REFERENCES ref_table_Name(ref_Table_colm_Name, ref_Table_colm_Name_2)   -- No comma no semicolon in the last line
);
```

### Way 2:
```sql
CREATE TABLE IF NOT EXISTS [table_name](
   -- table structure here (Same as above)
);
```

> #### SYMBOLES 
>
> - Yellow Key = PRIMARY KEY
> - Gray   KEY = UNIQUE


## Delete Table

### Way 1:
```sql
DROP TABLE [table_Name];   -- SHOW ERROR
```

### Way 2:
```sql
DROP TABLE IF EXISTS [table_Name];  -- Don't SHOW ERROR (Just give a warning)
```

## Examples for Practice
- Example 1 : [Link](https://github.com/TashinParvez/MySQL_From_Zero/tree/master/Data%20Definition%20Language%20(DDL)/Practice/Example%201)

