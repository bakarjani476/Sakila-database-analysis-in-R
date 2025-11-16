# Import the libraries and packages

library(DBI)
library(RMariaDB)
library(data.table)

# Connect R to Mysql database using dbconnect() function

con <- dbConnect(     # con is the connection object
  drv = MariaDB(),
  host = "localhost",
  port = 3306,
  user = "root",
  password = "bakarjappa476",
  dbname = "sakila"
)

# view tables

dbListTables(con)

head(film)

# It will give an error for this command:
# MySQL has a table named film,
# but tables inside MySQL do not automatically appear inside R
# —you must import them with an SQL query.

# So we will load the film table or any other table into R first.

film <- dbGetQuery(con, "SELECT * FROM film;")

# Or if we want only first 10 rows then:
film <- dbGetQuery(con, "select * from film limit 10;")

# Import the other tables
customer <- dbGetQuery(con, "select * from customer;")
actor <- dbGetQuery(con, "select * from actor;")

head(film)
head(actor)
head(customer)

# An important thing is that we can use the same syntax of SQL in R when we
# have connected it with R. But the condition is that we can only use this
# syntax or code inside dbGetQuery() function. For example;

result <- dbGetQuery(con, 
    "
    select dept, avg(salary) as avg_salary
    from emp
    where hire_year <= 2010
    group by dept
    having avg_salary > 50000
    order by avg_salay desc
    limit 5;
    "
)

# If we import the dataframe or data.table in R, then we use the R syntax, not SQL.

# To do this, convert the table(suppose film) into data.table(Recommeded for data analysis)

setDT(film)

# Let's write the same above query in R data.table syntax

# DT[hire_year <= 2010, .(avg_sal = mean(salary, na.rm = TRUE)), by = dept][avg_sal > 50000][order(-avg_sal)][1:5]


# Write a query to display all films that have a rating of PG and a 
#rental duration greater than 5 days.

setDT(film)

film[rating == "PG" & rental_duration > 5]

# Write a query to display the average rental rate of films, grouped by their rating.  

film[, .(avg_rental_rate = mean(rental_rate)), by = rating]

# Write a query to count the total number of films in each language.

# Import the language table in R
language <- dbGetQuery(con, "select * from language;")

head(language)

setDT(language)

merged_dt <- language[film, on = .(language_id)]

merged_dt[, .(total_films = .N), by = name]

# List the customers’ names and the store they belong to.

head(customer)

setDT(customer)
customer[, .(first_name, last_name, store_id)]

# Display the payment amount, payment date, and the staff member who processed each payment. 

# First let's bring the tables payment and staff in R

payment <- dbGetQuery(con, "select * from payment;")

staff <- dbGetQuery(con,"select * from staff;" )

# Set as data.table

setDT(payment)
setDT(staff)

merged_dt <- payment[staff, on =.(staff_id),nomatch = 0]
merged_dt[, .(amount, payment_date, first_name, last_name)]


# Find the films that are not rented.

inventory <- dbGetQuery(con, "select * from inventory;")
rental <- dbGetQuery(con, "select * from rental;")

setDT(inventory)
setDT(rental)

# rented films (film_id appearing in rentals)
rented_films <- inventory[rental, on = .(inventory_id), unique(film_id)]

# films NOT in rented list
never_rented <- film[!film_id %in% rented_films, .(film_id, title)]

never_rented

# Drawing plot using ggplot2 library

library(ggplot2)

# Average Rental rate by Film rating

avg_rate <- film[, .(avg_rental = mean(rental_rate)), by = rating]
avg_rate

p <- ggplot(avg_rate, aes(x = rating, y = avg_rental)) + geom_col(fill = "steelblue")+
  labs(
    title = "Avg Rental rate by Rating",
    x = "Film Rating",
    y = "Avg Rental"
  ) + 
  theme_minimal()


# save the plot in output folder

ggsave("output/avg_rental_rate_by_rating.png", p, width = 7, height = 5)
