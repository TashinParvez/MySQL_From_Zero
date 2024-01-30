# MySQL Notes Repository

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
