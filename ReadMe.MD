---------------------- DATABASE COMMANDS ----------------------------

     We need to go to www.mql.com
      - Download the community edition of mysql for the database
      - Download the community edition workbench for the interface
      - Establish the connection by entering the your db password 

    ---------------------- Select Clause ---------------------------

        USE sql_store;
        SELECT
          last_name,
          first_name,
          points,
          (points + 10) AS 'Discount factor'
        FROM customers
    
        SELECT DISTINCT state
        FROM customers
    
         NB: use AS to rename the name of the table
             The DISTINCT is to avoid duplicate in the table

    
    ---------------------- Where Clause ---------------------------

        USE sql_store;
        SELECT *
        FROM customers
        WHERE points > 3000; or state = 'VA'
        >, >=,  < , <=, =, != or <>
     
        Getting all the orders placed in the given date
        SELECT *
        FROM orders
        WHERE order_date > '2019-01-01';

    ---------------------- Where Clause ---------------------------

      The AND, OR, and NOT can be apply to the same logic
       SELECT * 
       FROM customers
       WHERE birth_date <= '1991-01-01 AND points <= 1000;

    ---------------------- Not, In ---------------------------
      SELECT *
      FROM customers
      WHERE state IN ('VA', 'PA') 
      or we can also use
      WHERE state NOT IN ('VA', 'PA') 

    ---------------------- Between ---------------------------

      SELECT *
      FROM customers
      WHERE points BETWEEN 1000 AND 3000 

    ---------------------- Like ---------------------------

      SELECT *
      FROM customers
      WHERE last_name LIKE 'b%'  // start with b
      
       'brush%' // Start with brush'
       '%brush%' // Brush in the middle
       '%y' // End with y
          'b____y' // start with a b and 4 characters and y
     
    NB: Like can also work with not
       NOT Like()
    Like the like word REGEXP is also powerful
    WHERE last_name REGEXP 'field'; ^ beginning $ the end and we can also use | for multiple
    WHERE last_name REGEXP '^field|mac|rose$'  // Start with field can contains mac and end with rose

    '[gim]e' = ge,ie, me
    '[a-h]e' = ae, be ...

    ---------------------- Null ---------------------------
  
     SELECT * 
     FROM customers 
     WHERE phone IS NULL  // or  IS NOT NULL


    ---------------------- Order by ---------------------------
     SELECT * 
     FROM customers 
     ORDER BY first_name DESC or ASC
    
    ---------------------- LIMIT ---------------------------
     SELECT * 
     FROM customers 
     LIMIT 300  // or LIMIT 6, 3 which mean select skip 6 record and pick the remaining 3

----------------------Multiple tables queries ----------------------------
   
     ---------------------- Inner join ---------------------------

       USE sql_store;
        SELECT
            order_id,
            o.customer_id,
            first_name,
            last_name
        FROM orders o
        INNER JOIN customers c
        ON o.customer_id = c.customer_id;

     // Join table from multiple databases
      
      Let say we have a database sql_store and sql_inventory
      USE sql_store
      SELECT *
      FROM order_items oi
      INNER JOIN sql_inventory.products p
      ON oi.product_id = p.product_id

      ------ We can also join a table with itself by using an alias-------

      SELECT 
         e.employee_id
         e.first_name
         m.first_name AS manager
      FROM employee e
      JOIN employee m
       on e.reports_to = m.employee_id

      ------ Joining multiple tables -------
      
      USE sql_store;
        SELECT
            O.order_id,
            O.order_date,
            C.first_name,
            C.last_name,
            OS.name AS status
        FROM orders O
        JOIN customers C
        ON O.customer_id = C.customer_id

     USE Sql_invoicing;
     SELECT * FROM payments p 
     JOIN clients c 
      ON p.client_id = c.client_id
     JOIN payment_methods pm
     ON p.payment_method = pm.payment_method_id 

