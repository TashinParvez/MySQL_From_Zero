# Data Manipulation Language (DML) Notes Repository

Welcome to my Data Manipulation Language (DML) notes repository!



## Insert DATA INTO Database Table

#### Way 1:
```sql
INSERT INTO [table_Name] (attrib_1, attrib_2, attrib_2, attrib_3, attrib_4)           
VALUES (coll1_val, coll2_val,  coll3_val, coll4_val)
                        
---- Dont forget to insert data in PRIMARY KEY
---- Follow the above serial

---- USE When you want to insert data into a few columns
```

#### Way 2:
```sql
INSERT INTO [table_Name] 
VALUES (coll1_val, coll2_val,  coll3_val, coll4_val)

----- FOLLOW table structure Serial [Coloum Order wise]

----- USE When you want to insert data in every column
```

#### Way 3:
```sql
INSERT INTO [table_Name] 
VALUES (coll1_val, coll2_val,  coll3_val, coll4_val), (coll1_val, coll2_val,  coll3_val, coll4_val), (coll1_val, coll2_val,  coll3_val, coll4_val)

---- USE when Multiple data insert  [Multiple rows input]
```




## UPDATE DATA INTO Database Table

#### Way 1:
```sql
UPDATE [table_name]
SET coll1 = value1, coll2 = value2, ......
WHERE [condition];

---- IF you dont write WHERE then all row's data will be update
```




## DELETE DATA INTO Database Table

#### Way 1:
```sql
DELETE FROM table_name
WHERE [condition];
```
