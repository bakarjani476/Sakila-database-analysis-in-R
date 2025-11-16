
# Sakila Database Analysis – R & Git Assignment

This project contains SQL-style data analysis performed in **R** using the `data.table` package.  
The assignment uses tables from the **MySQL Sakila database** and demonstrates data querying, joins,
aggregation, plotting, and Git version control.

---

## 📁 Project Structure

```

R-SQL Project/
│
├── SQL project in r.R        # All queries written using data.table in R
├── output/
│     └── plot.png      # Saved ggplot visual
└── README.md           # Project documentation

```

---

## 🔧 Technologies Used

- **R**
- **data.table**
- **ggplot2**
- **DBI** + **RMariaDB**
- **Git & GitHub**
- **MySQL Sakila Dataset**

---

## 📘 Tasks Completed

### **1. Films with rating 'PG' and rental duration > 5 days**
Data.table filtering to extract relevant films.

### **2. Average rental rate grouped by rating**
Grouped summary using `[, .(mean), by=]`.

### **3. Count total films in each language**
Join with the `language` table and aggregate using `.N`.

### **4. List customers and the store they belong to**
Join between `customer` and `store` tables.

### **5. Display payment amount, payment date, and staff member**
Join `payment` with `staff` using `data.table` syntax.

### **6. Films that are not rented**
Anti-join between `film` and `rental`.

### **7. Plotting (ggplot2)**
A bar plot was created for:
- **Average rental rate by film rating**

The plot is saved inside the `output/` folder.

---

## 📊 Example Plot

The plot generated in the assignment is saved here:

```

output/avg_rental_rate_plot.png

````

I saved plot using:

```r
ggsave("output/avg_rental_rate_plot.png", plot = p)
````

---

## 📝 Git Usage

The entire assignment was managed using Git:

* Initialized repository
* Staged and committed files
* Created a GitHub repository
* Pushed the work to GitHub
* Updated project with version control

Commands used include:

```bash
git init
git add .
git commit -m "Initial assignment commit"
git remote add origin <repo-link>
git push -u origin main
```

---

## 📂 How to Run the Code

1. Install required packages:

```r
install.packages(c("data.table", "ggplot2", "DBI", "RMariaDB"))
```

2. Connect to MySQL

```r
con <- dbConnect(
  RMariaDB::MariaDB(),
  host = "localhost",
  user = "root",
  password = "your_password",
  dbname = "sakila"
)
```

3. Load tables and run the queries inside `assignment.R`.

---

## 🙌 Author

**Muhammad Abu Bakar**
Data Analyst & Renewable Energy Data Science Enthusiast

