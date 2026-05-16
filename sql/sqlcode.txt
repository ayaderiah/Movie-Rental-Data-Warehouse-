
CREATE DATABASE IF NOT EXISTS movie_rental_dw;


USE movie_rental_dw;




CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,
    full_date DATE NOT NULL,
    day_name VARCHAR(20),
    month_number INT,
    month_name VARCHAR(20),
    year INT,
    quarter INT
);


CREATE TABLE dim_customer (
    customer_key INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    full_name VARCHAR(100),
    email VARCHAR(100),
    active BOOLEAN,
    create_date DATETIME
);

CREATE TABLE dim_film (
    film_key INT AUTO_INCREMENT PRIMARY KEY,
    film_id INT NOT NULL,
    title VARCHAR(255),
    description TEXT,
    release_year YEAR,
    rental_duration INT,
    rental_rate DECIMAL(4,2),
    length_minutes INT,
    replacement_cost DECIMAL(5,2),
    rating VARCHAR(10),
    category_name VARCHAR(50),
    language_name VARCHAR(50)
);


CREATE TABLE dim_store (
    store_key INT AUTO_INCREMENT PRIMARY KEY,
    store_id INT NOT NULL,
    manager_first_name VARCHAR(50),
    manager_last_name VARCHAR(50),
    city VARCHAR(100),
    country VARCHAR(100)
);


CREATE TABLE dim_staff (
    staff_key INT AUTO_INCREMENT PRIMARY KEY,
    staff_id INT NOT NULL,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    store_key INT,
    FOREIGN KEY (store_key) REFERENCES dim_store(store_key)
);


CREATE TABLE fact_rental (
    rental_key INT AUTO_INCREMENT PRIMARY KEY,
    rental_id INT NOT NULL,
    date_key INT NOT NULL,
    customer_key INT NOT NULL,
    film_key INT NOT NULL,
    store_key INT NOT NULL,
    staff_key INT NOT NULL,
    rental_duration_days INT,
    is_late_return BOOLEAN,
    
    FOREIGN KEY (date_key) REFERENCES dim_date(date_key),
    FOREIGN KEY (customer_key) REFERENCES dim_customer(customer_key),
    FOREIGN KEY (film_key) REFERENCES dim_film(film_key),
    FOREIGN KEY (store_key) REFERENCES dim_store(store_key),
    FOREIGN KEY (staff_key) REFERENCES dim_staff(staff_key)
);


CREATE TABLE fact_payment (
    payment_key INT AUTO_INCREMENT PRIMARY KEY,
    payment_id INT NOT NULL,
    date_key INT NOT NULL,
    customer_key INT NOT NULL,
    staff_key INT NOT NULL,
    rental_key INT,
    amount DECIMAL(5,2),
    
    FOREIGN KEY (date_key) REFERENCES dim_date(date_key),
    FOREIGN KEY (customer_key) REFERENCES dim_customer(customer_key),
    FOREIGN KEY (staff_key) REFERENCES dim_staff(staff_key),
    FOREIGN KEY (rental_key) REFERENCES fact_rental(rental_key)
);