# Class Performance
![](https://github.com/TashinParvez/MySQL_From_Zero/blob/Tashin/Data%20Definition%20Language%20(DDL)/Practice/Example%202/orders_items_normalized.png)


## Solution

###
```sql
CREATE TABLE items(
    item_id INT PRIMARY KEY,
    item_name VARCHAR(100),
    item_price NUMERIC
);
```


```sql
CREATE TABLE orders_items(
    item_id INT,
    order_id INT,
    
    CONSTRAINT it_ID
    FOREIGN KEY(item_id) REFERENCES items(item_id)

);
```


```sql
CREATE TABLE customers(
    customer_id INT,
    customer_phone VARCHAR(12),
    customer_email TEXT
);
```


```sql
CREATE TABLE orders(
    order_id INT PRIMARY KEY,
    order_date DATE,
    customer_id INT,
    
    CONSTRAINT cust_ID
    FOREIGN KEY(customer_id) REFERENCES customers(customer_id)
);
```

