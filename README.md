# SQL
# Hare Krishna 
# RAdhe Radhe

# Tutorial - https://www.postgresqltutorial.com/
# Data type - https://www.postgresql.org/docs/current/datatype.html
# pattern matching (like) - https://www.postgresql.org/docs/12/functions-matching.html
# aggregate function - https://www.postgresql.org/docs/current/functions-aggregate.html
# function formating - https://www.postgresql.org/docs/12/functions-formatting.html
# mathematical functions -  https://www.postgresql.org/docs/current/functions-math.html
# string functions - https://www.postgresql.org/docs/current/functions-string.html

-----------------------------------------------------------------------------------------------
# 1. Select -https://www.postgresqltutorial.com/postgresql-select/
it is the most common statement used, and it allows us to retrieve information from a table.
it combine with other statement to perform complex queries.

# Example-

      Select * from table_name;  // selects the all columns

      select column_name, c2 from table_name;

      select * from actor;
      select first_name, last_name from actor;

      select *  from city;


# Challenge Task-

situation - we want to send out a promotional email to our existing customers!

hint - use select statement to grab the first and lastname of every customer and their email address.

# Answer-

      select first_name, last_name, email from customer;

-----------------------------------------------------------------------------------------------
# 2. Distnict - https://www.postgresqltutorial.com/postgresql-select-distinct/

sometimes a table contain column with duplicate so if we want only unique/distinct values we use distinct

# distinct keyword
it used to retuen only distinct values in a column

# example

      Select distinct(column) from table;
 
      select distinct release_year from film;
 
      select distinct(rental_rate) from film;
 
 # Challenge
 
 What ratings type do we have available?
 
 # Ans
 
     select distinct rating from film;
 
 ---------------------------------------------------------------------------------------------

# 3. Count - https://www.postgresqltutorial.com/postgresql-count-function/

the count function returns the number of input rows that match a specific condition of a query.
we can apply count on a specific column or just pass count(*)

# example

      select count(name) from table;

# count with distinct

how many unique names are there in the table?

     select count(distinct name) from table;

1. count no of rows in table
2. select count unique values.

       select count(distinct amount) from payment;

----------------------------------------------------------------------------------------------
# 4. Where - https://www.postgresqltutorial.com/postgresql-where/

The Where statement allows us to to specify conditions on columns for the rows to be returned.

# basic syntax-
  
  select c1,c2 from table where conditions;
  
  for comparing conditions we use comparision operators
  
  comparision operator -- =,>,<,>=,<=, <> or != 
  logical operator - and, or , not
  
 # example
 
    select name,choice from table where name= 'David' and choice='Red'
 
    select count(title) from film
    where rental_rate>4 and replacement_cost>=19.99 and rating='R';

# challenge-

a customer forgot their wallet at our store! we need to track down their email and inform them so what is the email for customer with
name Nancy thomas?

       select * from customer;
       select email from customer where first_name='Nancy' and last_name= 'Thomas';

Q-2  find description of outlaw hanky


         select * from film;
         select description from film where title='Outlaw Hanky';

 Q-3  phone of customer on addrss 259 ipoh
 
         select phone from address where address= '259 Ipoh Drive';

--------------------------------------------------------------------------------------------------------------

# 5. OrderBy - https://www.postgresqltutorial.com/postgresql-order-by/

used to sort rows based on column value, in either ascending or descending order.

# syntax-

select c1,c2 from table orderby c1 asc/desc;

asc - dedault order (ascending order)
desc - descending order

# we can also order by multiple columns
* this make sense when one column has duplicate entries.

Ex-  select company,name,sales from table orderby company,sales;

     select * from customer order by first_name asc;
     select * from customer order by first_name desc;
     select * from customer order by store_id;

     select store_id,first_name, last_name from customer order by store_id,first_name desc;

# Challenge

Q1 what are the customer id of first 10 customers who do payment?

      select customer_id from payment
      order by payment_date 
      limit 10;

Q2 titles of 5 shortest movies?

     select title,length from film
     order by length 
     limit 5;

Q3 movie of length <=50

     select count(title) from film
     where length<=50;

----------------------------------------------------------------------------------------------------------
