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

![Clause Order](https://sp.postgresqltutorial.com/wp-content/uploads/2020/07/PostgreSQL-Having-1.png )
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

# 10. Aggregation Functions - https://www.postgresqltutorial.com/postgresql-aggregate-functions/

SQL provide a variety of aggregate functions.
the main idea behind an aggregate function is to take multiple inputs and return a single output.

link for more - https://www.postgresql.org/docs/current/functions-aggregate.html

most common are-

avg(), count(), max(), min(), sum(),round() etc.

# example-

       select min(replacement_cost) from film;
       select max(replacement_cost) from film;
       select avg(replacement_cost) from film;
       select round(avg(replacement_cost),2) from film;
       select sum(replacement_cost) from film;
       select max(replacement_cost), min(replacement_cost) from film;
       
 ------------------------------------------------------------------------------------------------------------
 
# 11. GroupBY - https://www.postgresqltutorial.com/postgresql-group-by/

It allows us to aggregate columns per some category.

we need to choose a categorical column to GROUP BY.
categorical columns  are non continous.

ex- class 1, class2 , etc. (can still be numerical)

# example 

      select category_col, agg(data_col) from table 
      group by category_col;

  group by clause must appear right after a from or where statement..

       select category_col, agg(data_col) from table 
       where category_col !='A' 
       group by category_col;
  
  
  In the select statement, columns must either have an aggregate function or be in the group by call.
  
    select company, division, sum(sales) from finance_table
    where division in ('marketing','transport')
    group by company,division
  
    select company, sum(Sales) from finance_table
    group by company
    order by sum(sales)
    limit 5
  
  
  ***************************************************
  
  more examples
  
  select customer_id, sum(amount) from payment
  group by customer_id
  order by sum(amount)
  
select customer_id, count(amount) from payment
group by customer_id
order by count(amount)

select customer_id, staff_id, sum(amount) from payment
group by staff_id, customer_id
order by customer_id

select staff_id, customer_id,sum(amount) from payment
group by staff_id, customer_id
order by staff_id,customer_id

select date(payment_date),sum(amount) from payment
group by date(payment_date)
order by sum(amount)

***************************************


# Challenge Question

Q1 how many payment each staff member handle ?

              select staff_id, count(*)  from payment
              group by staff_id

Q2  what is average replacement cost per mpaa rating?

    select * from film;
    select rating, round(avg(replacement_cost),2) from film
    group by rating
    order by avg(replacement_cost)

Q3 what are customer id of top 5 customer by total spend?

           select customer_id, sum(amount) from payment
           group by customer_id
           order by sum(amount) desc
           limit 5

--------------------------------------------------------------------------------------------------------------------
 
 # 12. Having - https://www.postgresqltutorial.com/postgresql-having/
 
 It allows us to filter after an aggregation has alreday taken place.

select company, sum(sales)
from finance
where company != 'Google'
group by company

we have already seen we can filter before executing the group by, but what if we want to filter based on sum(sales)

we can't use where to filter based off of aggregate results, because those happen after a where is executed

Solution is having

having allows us to use the aggregate result as a filter along with a group by

example

       select company, sum(sales)
       from finance
       where company != 'Google'
       group by company
       having sum(sales) >  1000


       select customer_id, sum(amount) from payment
       group by customer_id
       having sum(amount) > 100

       select store_id, count(*) from customer
       group by store_id
       having count(*) > 300


************************************

# Challenge

Q1 customer having 40 or more transaction got platinum .. what customer_ids are eligible?

        select customer_id, count(amount) from payment
        group by customer_id
        having count(amount) >= 40;


Q2 customer ids of cust who have spent more than $100 in payment transactions with our staff_id member 2?

         select customer_id, sum(amount) from payment
         where staff_id = 2
         group by customer_id
         having sum(amount)> 100 

----------------------------------------------------------------------------------------------------------------- 
 
# 13.  AS - https://www.postgresqltutorial.com/postgresql-alias/

it allows us to create an alias for a column or result.

Syntax

    select sum(column) as new_name from table

# example

select amount as rental_price from payment;

* The as operator gets executed at very end of query , we cant use alias inside where operator.

        select customer_id, sum(amount) as total_spent from payment
        group by customer_id

       select customer_id, sum(amount) as total_spent from payment
       group by customer_id
       having sum(amount) > 100

-----------------------------------------------------------------------------------------------------------------

# JOINS - https://www.postgresqltutorial.com/postgresql-joins/

----------------------------------------------------------------------------------------------------------------
# 14. Inner Join - https://www.postgresqltutorial.com/postgresql-inner-join/

Join allows us to combine multiple tables together


# an inner join will reslt with the set of records that match in both tables.

Syntax

select * from tableA
inner join tableB
on tableA.col_match = tableB.col_match

simple join also means inner join

in inner join table order won't matter.

# Example-

        select * from payment
        inner join customer
        on payment.customer_id= customer.customer_id

        select payment_id, payment.customer_id, first_name, last_name 
        from customer
        inner join payment
        on payment.customer_id= customer.customer_id

----------------------------------------------------------------------------------------------------

# 15.  Full Outer JOin  -  https://www.postgresqltutorial.com/postgresql-full-outer-join/

* there are few types of Outer Joins
* they will allow us to specify how to deal with values only present in one of the tables being joined.

## Full Outer Join

Select * from t1
full outer join t2
on t1.col = t2.col;

fill null in misclarifying values... fill everything

         select * from payment
         full outer join customer
         on payment.customer_id= customer.customer_id

with where

         select * from t2
         full outer join t1
         on t1.col=t2.col
         where t1.id is null or t2.id is null


         select * from payment
         full outer join customer
         on payment.customer_id= customer.customer_id
         where customer.customer_id is null
         or payment.payment_id is null

---------------------------------------------------------------------------------------------------------------------

# 16. Left Outer Join - https://www.postgresqltutorial.com/postgresql-left-join/

 It join results in set of records that are in left table, if no match with right , then table is null.

select * from t1
left outer join t2
on t1.col = t2.col;

# example

     select * from registerations 
     left outer join logins
     on registerations.name =  logins.name

     select * from registerations
     left outer join logins
     on registerations.name =  logins.name
     where logins.log_id is null


     select film.film_id, film.title, inventory_id, store_id
     from film
     left join inventory on
     inventory.film_id= film.film_id


     select film.film_id, film.title, inventory_id, store_id
     from film
     left join inventory on
     inventory.film_id= film.film_id
     where inventory.film_id is null
   
------------------------------------------------------------------------------------------------------------------

# 17. Right Outer JOin -  https://www.postgresqltutorial.com/postgresql-right-join/

 Right Join is same as left Join
 
 It join results in set of records that are in right table, if no match with left , then table is null.

       select * from t1
       right outer join t2
       on t1.col= t2.col


       select * from t1
       right outer join t2
       on t1.col= t2.col
       where t1.id is null

       select film.film_id, film.title, inventory_id, store_id
       from film
       right join inventory on
       inventory.film_id= film.film_id

---------------------------------------------------------------------------------------------------------------------

# 18. Union - https://www.postgresqltutorial.com/postgresql-union/

  
# Union

it  is used to combine the result set of two or more select statements
pasting of result together.

```
select c1 from t1
union 
select c2 from t2
```
---------------------------------------------------------------------------------------------------------------------

# 19. Join Challenge -

## Q1 We have to alert our customers through email about changes in tax in California
  what are emails of customers live in California

``` 
select district, customer.email from customer
inner join address
on customer.address_id= address.address_id
where address.district = 'California'
```

## Q2 List of movie of Nick Wahlberg

```
select title, first_name, last_name from film_actor
inner join actor
on actor.actor_id= film_actor.actor_id
inner join film
on film_actor.film_id=film.film_id
where first_name='Nick' and last_name = 'Wahlberg'
```
---------------------------------------------------------------------------------------------------------------------------

# 20. TimeStamps and Extract -  https://www.postgresqltutorial.com/postgresql-timestamp/
#                               https://www.postgresqltutorial.com/postgresql-extract/

commands that report back time and date information.

Time = contains only time

Date= contains only date

Timestamp =  contains date and time

Timestampz = contains date, time and timezone

timezone, now, timeofday, current_time, current_date

#ex-
```
show all
show timezone

select now()-  timestamp with time zone

select timeofday() - today day time

select current_date
```

*************************************************
# Extract()

-- allows you to extract or obtain a sub component of a date value

year, month, day, week, quarter

extract(year from date_col)

# Age() - calculate and returns the current age given a timestamp

age(date_col)

# To_char()- convert date types to text

to_char(date_col,'mm-dd-yyyy')

*************************************************
```
select extract(year from payment_date) as my_year from payment

select extract(month from payment_date) as pay_month from payment

select age(payment_date) from payment

select to_char(payment_date,'mm-yy') from payment
```

*************************************************

# Challenge tasks-

see documentation for more
Q1 which months did payment occur?

```select distinct(to_char(payment_date,'month')) from payment;```

Q2 How many payments occure on  monday?

```select count(*) from payment where extract(dow from payment_date)=1```

-----------------------------------------------------------------------------------------------------------------------------------------

# 21. Mathematical functions and operators - https://www.postgresqltutorial.com/postgresql-math-functions/

```
select round(rental_rate/replacement_cost,2)*100 
from film

select 0.1 * replacement_cost as deposit from film
```

-----------------------------------------------------------------------------------------------------------------------------------------

# 22. String -  https://www.postgresqltutorial.com/postgresql-string-functions/ 

```
select length(first_name) from customer

select (first_name ||' '|| last_name) as name from customer

select (upper(first_name) ||' '|| last_name) as name from customer

select first_name || last_name || '@gmail.com' from customer

select lower(left(first_name,1)) || lower(last_name) || '@gmail.com' as customer_email from customer
```
-------------------------------------------------------------------------------------------------------------------------------------------

# 23. Sub Query - https://www.postgresqltutorial.com/postgresql-subquery/

A sub query allows you to construct complex queries, essentailly performing a query on the results of another query.

syntax is simple and include two select staetement.

# standard query

select avg(grade) from test_scores

ex- select student, grade from test_scores where grade > (select avg(grade) from test test_scores)

select student, grade from test_scores where student in (select student from honor_roll_table)

# Exists

the exists operator is used to test for existence of rows in a subquery

typically a subquery  is passed in the exists() function to check if any rows are returned with the subquery.

```
select column_name from table_name
where exists (select column_name from table_name where condition);

select title,rental_rate 
from film
where rental_rate>(select avg(rental_rate) from film)

select * from rental
where return_date between '2005-05-29' and '2005-05-30'

select inventory.film_id
from rental
inner join inventory on inventory.inventory_id = rental.inventory_id
where return_date between '2005-05-29' and '2005-05-30'

select film_id,title from film
where film_id in
(select inventory.film_id
from rental
inner join inventory on inventory.inventory_id = rental.inventory_id
where return_date between '2005-05-29' and '2005-05-30')

select first_name, last_name
from customer as c
where exists
(select * from payment as p
where c.customer_id=p.customer_id
and amount>11)
```

---------------------------------------------------------------------------------------------------------------------------------------------------------------

# 24. Self Join - https://www.postgresqltutorial.com/postgresql-self-join/

 A self Join is a query in which a table is joined to itself
 Self-joins are useful for comparing values in a column of rows within the same table.

it creates two copies of same table and perform join operation
use alias during self join

syntax-

```
select tablea.col, tableb.col
from table as tablea
join table as tableb on
tablea.some_col = tableb.other_col

select title,length from film
where length=117

select f1.title, f2.title, f1.length
from film as f1
inner join film as f2 on
f1.film_ID != f2.film_id
and f1.length= f2.length
```
------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 25. Data Types - https://www.postgresqltutorial.com/postgresql-data-types/

## Boolean

  True or False
  
## Character

  char, varchar, and text
  
## Numeric

  integer and floating point number
  
## Temporal

  date, time, timestamp, and interval
  
 other types-
 
 uuid
 array
 json
 key value pair
 network address and geometric data
 
---------------------------------------------------------------------------------------------------------------------------------------------------
 
# 26. Primary and Foreign key -  https://www.postgresqltutorial.com/postgresql-primary-key/
#                                https://www.postgresqltutorial.com/postgresql-foreign-key/

## Primary key-
It is a column or a group od column to identify a row uniquely in table.

for ex - customer_id in customer table

## Foreign key-

It is a field or group of fileds in a table that uniquely identifies a row in another table.
It is defined in a table that references to the primary key of other table


table with foreign key is referencing table or child table.
table to which foreign key references is parent table.
a table can have multiple foreign keys depending upon its relation with other tables.

-----------------------------------------------------------------------------------------------------------------------------------------------------

# 27. Constriants -
 
 Rules enforced on data columns on table
these are used to prevent invalid data from being entered into database.
this ensures accuracy and reliability of data in database.

Column constraint
table constraint

not null constraint
unique constaint
primary key
foreign key
check constraint - ensure all value satisfy certain condition
exclusion constraint
check(condition)
references

-------------------------------------------------------------------------------------------------------------------------------------------------------

# 28. Create Table - https://www.postgresqltutorial.com/postgresql-create-table/

create table table_name(
  column_name type column_constraint,
  column_name type column_constraint,
  table_constraint table_constraint
  )inherits existing_table_name;
  
  ###  Serial - create a sequence of object and it is prfect for primary key
  
 ```
  create table players(
  player_id serial primary key,
  age smallint not null);
  
  create table account(
  user_id serial primary key,
	username varchar(50) unique not null,
	password varchar(50) not null,
	email varchar(250) unique  not null,
	created_on timestamp unique not null,
	last_login timestamp
)
  
  create table job (
  job_id serial primary key,
  job_name varchar(200) unique not null
)

create table account_job(
  user_id integer references account(user_id),
	job_id integer references job(job_id),
	hire_data timestamp
)
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 29. Insert -  https://www.postgresqltutorial.com/postgresql-insert/

insert allows us to add rows to a table

syntax

insert into table(c1,c2,....)
select c1,c2
from another_table
where condition;

```
insert into account(user_name,password,email, created_on)
values
('Ritik','passw','ritik@mail.com',current_timestamp)

insert into job(job_name)
values
('bhkti')

insert into account_job(user_id, job_id, hire_data)
values
(1,1, current_timestamp)
```
---------------------------------------------------------------------------------------------------------------------------------------------------------------

# 30. Update - https://www.postgresqltutorial.com/postgresql-update/

### the update value allows us to chnage value of columns in a table.

syntax

update table
set col1= val,
    col2= val2,...
    where 
    condition;
    
update account
set last_login= current_timestamp
where last_login is null;
     
     
### using another table value (update join)

```
update tablea
set orriginal_col= tableb.new_col
from tableb
where tablea.id = tableb.id


update account_job
set hire_data = account.created_on
from account
returning account_job.user_id
```

# return affected rows

```
update account
set Last_login = created_on
returning account_id,last_login
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 31. Delete- https://www.postgresqltutorial.com/postgresql-delete/

we can use the delete clause to remove rows from a table

for ex-

delete from table where row_id=1

we can delete rows based on their presence in other tables.

delete from tablea
using tableb
where tablea.id= tableb.id


delete from table //delete all rows from table

we can also return using delete like update

```
delete from job 
where job_name= 'cow_boy'
returning job_id, job_name
```

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 32. Alter Table - https://www.postgresqltutorial.com/postgresql-alter-table/

The Alter Clause allows for changes to an existing table structure

  adding, dropping, or renaming columns
  changing a column's data type
  set default values for column
  add check constraint
  rename table
  
  
  alter table table_name
  add column new_col type
  
  alter table table_name
  alter column col_name
  set not null
  
  ```
  create table information(
  info_id serial primary_key,
  title varchar(500) not null,
  person varchar(50) not null unique
  );
  
  alter table information rename to new_info;
  
  alter table new_info
  rename column person to people
  
  
  insert into new_info(title)  //error
values
('some new title')

alter table new_info
alter column people drop not null
```
----------------------------------------------------------------------------------------------------------------------------------------------------------------
# 33. Drop - https://www.postgresqltutorial.com/postgresql-drop-column/

complete removal of column in table

alter table  table_name
drop column col_name cascade

check existnce to avoid error

alter table table_name
drop column if exists col_name

```
alter table new_info
drop column people

alter table new_info
drop column if exists people
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 34. Check - https://www.postgresqltutorial.com/postgresql-check-constraint/

The Check constraint allows us to create more customized constraints that adhere to a certain condition.
such as making sure all inserted integer values fall below a certain threshold.

Create table example(
 ex_id serial primary key,
 age smallint check (age > 21),
 parent_age smallint check(
 parent_age > age)
 );
 
 
 ```
 Create table employees(
 emp_id serial primary key,
 first_name varchar(50) not null,
 last_name varchar(50) not null,
  birthdate date check (birthday> '1900-01-01'),
	hire_date date check (hire_date > birthdate),
	salary integer check (salary > 100)
)

 insert into employees(first_name,last_name,
					 birthdate, hire_date,
					 salary)
values
('ritik','dagar','2000-01-27','2018-02-03',1000)
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 35. Case - https://www.postgresqltutorial.com/postgresql-case/

we can use case statement to only execute sql code when certain conditions are met.
this is very similar to if/else statements in other programming languages.

syntax-

CASE
   when condition1 then result1
   when condition2 then result2
   else some_other_result
END

ex-

```
select a,
case when a=1 then 'one'
     when a=2 then 'two'
  else 'other'
  end
  from test;
  
 
select customer_id,
case
    when (customer_id<=100) then 'premium'
	when (customer_id between 100 and 200) then 'plus'
	else 'normal'
end
from customer


select customer_id,
case customer_id
    when 1 then 'premium'
	when 2 then 'plus'
	else 'normal'
end as results
from customer

select rental_rate,
sum(case rental_rate
     when 0.99 then 1
	 else 0
end) as bargains,
sum(case rental_rate
     when 2.99 then 1
	 else 0
end) as regular
from film
group by rental_rate


select rental_rate,
sum(case rental_rate
     when 0.99 then 1
	 else 0
end) as bargains,
sum(case rental_rate
     when 2.99 then 1
	 else 0
end) as regular,
sum(case rental_rate
     when 4.99 then 1
	 else 0
end) as premium
from film
group by rental_rate
```

# Challenge task-
various amounts of films per movie rating

```
select rating,
sum(case rating
 when 'R' then 1
 else 0
 end) as r,
 sum(case rating 
 when 'PG' then 1
 else 0
 end) as pg,
 sum(case rating
 when 'PG-13' then 1
 else 0
 end) as pg13
 from film
 group by rating
 ```
 ---------------------------------------------------------------------------------------------------------------------------------------------------------

# 36. Coalesce -  https://www.postgresqltutorial.com/postgresql-coalesce/

It accepts unlimited no of arguments, it returns first argument that is not null.
-> coalesce (arg1, arg2, ...., arg_n)

ex-
 select coalesce(1,2)  _>1
 select coalesce(null,2,3) -> 2
 
 
 ex-
 ```
 select item, (price - coalesce(discount, 0)) as final from table
```
-------------------------------------------------------------------------------------------------------------------------------------------------------
# 37. Cast - https://www.postgresqltutorial.com/postgresql-cast/

It allows us to convert one data type into another.

Type convert should be reasonable.

select cast('5' as integer)

select '5':: Integer

select cast(date as timestamp) from table

example-

```
select char_length(cast(inventory_id as varchar)) from rental
```

---------------------------------------------------------------------------------------------------------------------------------------------------------
# 38. Nullif - https://www.postgresqltutorial.com/postgresql-nullif/

passed 2 arguments

return null if both are equal else returns first argument

#ex-

create table dept;

```
select (
sum(case when department='cse' then 1 else 0 end)/
	sum(case when department='head' then 1 else 0 end)
) as department_ratio
from depts

select (
sum(case when department='head' then 1 else 0 end)/
	nullif(sum(case when department='cse' then 1 else 0 end),0)
) as department_ratio
from depts
```
----------------------------------------------------------------------------------------------------------------------------------------------------------
# 39. Views - https://www.postgresqltutorial.com/postgresql-views/

during project we have combination of tables and conditions
instead of trying same query again and again we can create view to quickly see the query with simple call.


a view is a database object that stored query.
it is virtual table
it doesn't store data physically but stores query.

we can also update and alter existing views

create view customer_info as
select first_name,last_name,address from customer
inner join address
on customer.address_id = address.address_id

```
select * from customer_info

create or replace view customer_info as 
select first_name,last_name,address,district from customer
inner join address
on customer.address_id = address.address_id

alter view customer_info rename to c_info

drop view c_info
```
---------------------------------------------------------------------------------------------------------------------------------------------------------
# 40. Import and export -  https://www.postgresqltutorial.com/import-csv-file-into-posgresql-table/
#                          https://www.postgresqltutorial.com/export-postgresql-table-to-csv-file/

how to import .csv file to an existing table?

file should be compatible with sql
you must provide 100% correct file path

import command doesnt create table for us
it assumes a table is already created.


https://www.postgresql.org/docs/12/sql-copy.html

https://www.enterprisedb.com/postgres-tutorials/how-import-and-export-data-using-csv-files-postgresql

---------------------------------------------------------------------------------------------------------------------------------------------------------

# 41. Pgsql with Python - https://www.postgresqltutorial.com/postgresql-python/

# 42. Triggers - https://www.postgresqltutorial.com/postgresql-triggers/

# 43. Indexes - https://www.postgresqltutorial.com/postgresql-indexes/

# 44. Administration - https://www.postgresqltutorial.com/postgresql-administration/

-----------------------------------------------------------------------------------------------------------------------------------------------------------
# for more see postgresql tutorial and documentation  ....

# Thank You

# Radhe Radhe 
