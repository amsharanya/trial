mysql> create database if not exists ecommerce;
Query OK, 1 row affected (0.093 sec)

mysql> use ecommerce
Database changed
mysql> CREATE TABLE customers (
    ->     customer_id SERIAL PRIMARY KEY,
    ->     name VARCHAR(100) NOT NULL,
    ->     email VARCHAR(255) UNIQUE NOT NULL
    -> );
Query OK, 0 rows affected (0.557 sec)

mysql> CREATE TABLE products (
    ->     product_id SERIAL PRIMARY KEY,
    ->     name VARCHAR(100) NOT NULL,
    ->     price DECIMAL(10, 2) NOT NULL
    -> );
Query OK, 0 rows affected (0.429 sec)

mysql> CREATE TABLE orders (
    ->     order_id SERIAL PRIMARY KEY,
    ->     customer_id INT NOT NULL REFERENCES customers(customer_id),
    ->     order_date TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
    -> );
Query OK, 0 rows affected (0.493 sec)
mysql> CREATE TABLE order_items (
    ->     order_item_id SERIAL PRIMARY KEY,
    ->     order_id INT NOT NULL REFERENCES orders(order_id),
    ->     product_id INT NOT NULL REFERENCES products(product_id),
    ->     quantity INT NOT NULL CHECK (quantity > 0),
    ->     price_at_time_of_order DECIMAL(10, 2) NOT NULL,
    ->     UNIQUE(order_id, product_id)
    -> );
Query OK, 0 rows affected (0.512 sec)
