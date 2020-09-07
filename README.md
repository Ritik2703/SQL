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

# 6. LIMIT - https://www.postgresqltutorial.com/postgresql-limit/

it allows us to limit the no of rows returned for a query.
useful to view top rows to see table layout
ūśeful with combination with order by.
it is last command to be executed.

ex-

     select * from payment limit 3; // return top 3 rows

     select * from payment
     where amount != 0.00
     order by payment_date desc
     limit 5;
   
--------------------------------------------------------------------------------------------------------------

# 7. BETWEEN - https://www.postgresqltutorial.com/postgresql-between/

it is used to match a value against range of values:  value between low and high.
it is same as value>=low and value <= high

# NOT BETWEEN
 value not between high and low
 same as value< low or value> high
 
 we can use between to compare between dates also.
 
 # ex-
 
         select count(*) from payment
         where amount between 8 and 9
 
         select * from payment 
         where payment_date between '2007-02-01' and '2007-02-15'
 
 ------------------------------------------------------------------------------------------------------------
 
 # 8. IN - https://www.postgresqltutorial.com/postgresql-in/
 
 we use in to check if value included in list of multiple options

# ex-

     select color from table where color in ('red','blue', 'green')
     select color from table where color not in ('red', 'blue')

     select * from payment
     where amount in (0.99, 1.98, 1.99)

     select count(*) from payment
     where amount not in (0.99, 1.98, 1.99)

     select * from customer
     where first_name in ('ritik','John','Julie')

-------------------------------------------------------------------------------------------------------------

# 9. Like (use for pattern matching) - https://www.postgresqltutorial.com/postgresql-like/

for ex- mails end with @gmail.com , name starting with a, etc.

Like operator allows us to perform pattern matching against string data with use of wildcard characters:

Percent %  - matches any sequence of characters

Underscore _ - matches any single character.

example

all name starts with A , a

    where name like 'A%'
    where name like 'a%'

    where name alike '%a'

# Note - Like is case sensitive and Ilike is case insensitive.

# using underscrore allow us to replace just a single character 
ex- get all mission Impossible film

     where title like 'Mission Impossible _'
     
we can use multiple underscores

ex- ritik23, ritik45
       where value like 'ritik_ _'

 
can also use for more complex pattern like

cheryl, theresa, sherri

     where name like '_her%'

# Example

               select * from customer
               where first_name like 'J%'

               select * from customer
               where first_name ilike 'j%'

               select count(*) from customer
               where first_name ilike 'j%' and last_name like 'S%'

               select * from customer
               where first_name ilike '%er%'

              select * from customer
              where first_name ilike '_her%'

              select * from customer
              where first_name not like '_her%'

              select * from customer
              where first_name ilike 'a%' and last_name not ilike 'b%'
              order by last_name

----------------------------------------------------------------------------------------------------------

