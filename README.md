Q1 - -- Retrieve the total number of orders placed.

SELECT 
    COUNT(order_id) AS total_orders
FROM
    orders;

RESULT :
![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/d66b137f312aece9106c37ba1807eb85553afac7/pizza_sales/Screenshot%202024-08-31%20184434.png).


Q2 -- Calculate the total revenue generated from pizza sales.

SELECT 
ROUND(SUM(order_details.quantity * pizzas.price),
            2) AS total_sales
FROM order_details
JOIN pizzas
ON pizzas.pizza_id = order_details.pizza_id
    
RESULT:
![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/2a18337a6b0029c1be0f8c00a3b5cae4fd4eb0e8/pizza_sales/Screenshot%202024-08-31%20192622.png)

