# Movie Rental Data Warehouse

This project is a Data Warehouse project built using the **Sakila Movie Rental Database**.

The idea of the project is to take the rental system data from the normal database `(OLTP)` and transform it into a warehouse database `(OLAP)` that can be used for analysis and reporting.

In the project, I designed a **Star Schema**, created fact and dimension tables, applied the ETL process, and generated some visual reports to better understand the data.

---

# Project Objectives

* Build a Data Warehouse for the Sakila database
* Convert transactional data into analytical data
* Design the warehouse using Star Schema
* Apply ETL steps using Python
* Create reports and data analysis

---

# Technologies Used

* MySQL Server 
* MySQL Workbench
* Python
* Pandas
* SQLAlchemy
* Jupyter Notebook
* Matplotlib
* GitHub

---

# Database Design

## Dimension Tables

* `dim_date`
* `dim_customer`
* `dim_film`
* `dim_store`
* `dim_staff`
* `dim_category`
* `dim_actor`
* `dim_location`

## Fact Tables

* `fact_rental`
* `fact_payment`

---

# ETL Process

## Extract

The data was extracted from the original `sakila` database.

## Transform

During this step, the data was cleaned and prepared before loading it into the warehouse database.

Some transformations included:

* Cleaning missing data
* Creating surrogate keys
* Combining related tables
* Calculating rental duration
* Calculating delayed returns

## Load

After the transformation step, the data was loaded into:

```sql id="6lq82n"
movie_rental_dw
```

---

# Business Analysis

Using the warehouse, different types of analysis can be done, such as:

* Most rented movies
* Monthly revenue analysis
* Store performance
* Customer behavior
* Late return analysis
* Revenue by country and city

---

# Project Structure

```bash id="4x9h9n"
Movie-Rental-Data-Warehouse/
│
├── SQL/
│   ├── sqlcode.sql
│   └── sqlcode.txt
│
├── ETL/
│   └── etl_process.ipynb
│
├── Images/
│   ├── erd.png
│   ├── film_categories.png
│   ├── monthly_revenue.png
│   └── top_customers.png
│
├── Report/
│   └── reportdw.pdf
│
└── README.md
```



