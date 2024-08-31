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

Q3 -- Identify the highest-priced pizza.

SELECT 
    pizza_types.name, pizzas.price
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY pizzas.price DESC
LIMIT 1;

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/6c9b43234aedc9172a2dfa334ded7905d7d35601/pizza_sales/Screenshot%202024-08-31%20193910.png)

Q4 -- Identify the most common pizza size ordered.

SELECT 
    pizzas.size,
    COUNT(order_details.order_details_id) AS order_count
FROM
    pizzas
        JOIN
    order_details ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizzas.size
ORDER BY order_count DESC;

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/1e40ac91f2fca84dae843ce49dbef6fe1f2b3196/pizza_sales/Screenshot%202024-08-31%20194440.png)

Q5 -- List the top 5 most ordered pizza types along with their quantities.
 
SELECT 
    pizza_types.name, SUM(order_details.quantity) AS quantity
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
        JOIN
    order_details ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY quantity DESC
LIMIT 5;

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/5e601eae2c3f4f608e06cbfc5fdc22db1d8b202c/pizza_sales/Screenshot%202024-08-31%20195115.png)

Q6 -- Join the necessary tables to find the total quantity of each pizza category ordered.

SELECT 
    pizza_types.category,
    SUM(order_details.quantity) AS quantity
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
        JOIN
    order_details ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizza_types.category
ORDER BY quantity DESC; 

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/c9ad8c29cf19e1d06415d55d7507e95ad89bed9a/pizza_sales/Screenshot%202024-08-31%20195334.png)

Q7 -- Determine the distribution of orders by hour of the day.

SELECT 
    HOUR(order_time), COUNT(order_id)
FROM
    orders
GROUP BY HOUR(order_time);

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/984b5167ec941a96405916cd75248c3459212702/pizza_sales/Screenshot%202024-08-31%20195853.png)

Q8 -- Join relevant tables to find the category-wise distribution of pizzas.

select category , count(name) from pizza_types
group by category;

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/603c3cdf007f0f6dfc9b706514af9a96c5fcd64d/pizza_sales/Screenshot%202024-08-31%20200211.png)

Q9 -- Group the orders by date and calculate the average number of pizzas ordered per day.

SELECT 
    ROUND(AVG(quantity), 0) as avg_pizza_ordered_per_day
FROM
    (SELECT 
        orders.order_date, SUM(order_details.quantity) AS quantity
    FROM
        orders
    JOIN order_details ON orders.order_id = order_details.order_id
    GROUP BY orders.order_date) AS order_quantity;

RESULT:

![Image Alt](https://github.com/biswaranjandash/sql-project-for-pizza-sale-/blob/3fdab11a8e6e9b144d806c7044de7c007beb2e18/pizza_sales/Screenshot%202024-08-31%20200512.png)

Q10 -- Determine the top 3 most ordered pizza types based on revenue.

select pizza_types.name ,
sum(order_details.quantity * pizzas.price) as revenue
from pizza_types join pizzas
on pizzas.pizza_type_id = pizza_types.pizza_type_id
join order_details
on order_details.pizza_id = pizzas.pizza_id
group by  pizza_types.name order by revenue desc limit 3 ;

RESULT:



