# Online-Shopping-System-Database
CREATE DATABASE OnlineShoppingDB;
USE OnlineShoppingDB;
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE Addresses (
    address_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    address_line VARCHAR(255) NOT NULL,
    city VARCHAR(50),
    state VARCHAR(50),
    zip_code VARCHAR(10),
    country VARCHAR(50),
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE
);
CREATE TABLE Categories (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) NOT NULL
);
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    category_id INT,
    product_name VARCHAR(150) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock_quantity INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2) NOT NULL,
    order_status VARCHAR(50) DEFAULT 'Pending',
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
CREATE TABLE Order_Items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
CREATE TABLE Payments (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    payment_method VARCHAR(50),
    payment_status VARCHAR(50),
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id)
);
CREATE TABLE Cart (
    cart_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
INSERT INTO Users (full_name, email, password, phone)
VALUES
('John Doe', 'john@example.com', 'john123', '9876543210'),
('Alice Smith', 'alice@example.com', 'alice123', '9123456780');
INSERT INTO Addresses (user_id, address_line, city, state, zip_code, country)
VALUES
(1, '123 Main Street', 'New York', 'NY', '10001', 'USA'),
(2, '456 Park Avenue', 'Los Angeles', 'CA', '90001', 'USA');
INSERT INTO Categories (category_name)
VALUES
('Electronics'),
('Clothing'),
('Books');
INSERT INTO Products (category_id, product_name, description, price, stock_quantity)
VALUES
(1, 'Smartphone', 'Android smartphone with 5G', 499.99, 50),
(1, 'Laptop', '15-inch laptop, 8GB RAM', 899.99, 30),
(2, 'T-Shirt', 'Cotton round-neck T-shirt', 19.99, 100),
(3, 'SQL Book', 'Learn SQL from scratch', 29.99, 40);
INSERT INTO Orders (user_id, total_amount, order_status)
VALUES
(1, 519.98, 'Confirmed'),
(2, 29.99, 'Pending');
INSERT INTO Order_Items (order_id, product_id, quantity, price)
VALUES
(1, 1, 1, 499.99),
(1, 3, 1, 19.99),
(2, 4, 1, 29.99);
INSERT INTO Payments (order_id, payment_method, payment_status)
VALUES
(1, 'Credit Card', 'Paid'),
(2, 'UPI', 'Pending');
INSERT INTO Cart (user_id, product_id, quantity)
VALUES
(1, 2, 1),
(2, 3, 2);
SELECT * FROM Users;
SELECT * FROM Products;
SELECT * FROM Orders;
SELECT * FROM Order_Items;

