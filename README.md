# E-commerce Data Cleaning and Analysis Using SQL and Python

## Porject overview

This project demonstrates my skills in data cleaning, data integrity checking, and basic analytics using SQL, with visualization integration in Python. I used SQL for data preparation and data cleaning, followed by exploratory data analysis (EDA) to gain insights into customer purchasing behaviors. Python was used to create visualizations that complement SQL insights, showcasing my ability to bridge data processing and data science with these tools.

### Data Validation and Quality Checks
Checking for Duplicates: Ensuring that the rows in table are unique where required. Also checking for duplicates based on primary columns like order_id and product_id.

CREATE TABLE ecomm_summary AS 
SELECT
	c.Customer_Id,
	c.Customer_Name,
	o.order_date,
	o.quantity,
    p.product_id,
	p.Category AS product_category,
	p.cost AS product_price,
    p.Product AS product_name,
	e.order_number AS order_id,
    e.brand

FROM 
	customers AS c
JOIN 
	orders AS o ON c.Customer_Id = o.customer_id
JOIN 
	products AS p ON o.product_id = p.Product_id
JOIN 
	online_ecommerce AS e ON o.order_number = e.order_number

####step 2 

SELECT * FROM ecomm_summary LIMIT 10;

SELECT order_id, product_id, COUNT(*)
FROM ecomm_summary 
GROUP BY order_id, product_id
HAVING count(*) > 1;

SELECT * FROM ecomm_summary
WHERE customer_id IS NULL OR product_id IS NULL OR Customer_Name IS NULL OR order_id IS NULL;

SELECT product_id, SUM(quantity) AS total_sales
FROM ecomm_summary
GROUP BY product_id;

CREATE INDEX idx_order_id ON ecomm_summary(order_id);
CREATE INDEX idx_product_id ON ecomm_summary(product_id);

EXPLAIN SELECT * FROM ecomm_summary WHERE product_id = '512';

Saved and exported the data as a csv file, ready for python data visualization. 


