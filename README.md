# 🎬 Cinema Seat & Ticket Booking System Using MySQL

A MySQL database project designed to manage movies, cinema screens, seats, show schedules, customers, ticket bookings, and payments using relational database concepts and advanced SQL features.


---

## 📌 Project Overview

The Cinema Seat & Ticket Booking System is a database management project that simulates the core operations of a cinema ticket booking platform. It maintains movie information, screen details, seating arrangements, show schedules, customer records, bookings, and payment information.

The project demonstrates how a relational database can maintain data integrity, manage seat reservations, retrieve information efficiently, and generate booking and revenue reports.

## 🎯 Objectives

- Design a relational database for cinema ticket booking.
- Manage movies, screens, seats, and show schedules.
- Store customer details and booking information.
- Track booking status and payment status.
- Prevent duplicate seat assignments for the same show.
- Generate reports using SQL queries, views, and stored procedures.
- Implement data validation using constraints and triggers.
- Improve query performance using indexes.

## 🛠️ Technologies Used

- **Database:** MySQL
- **Database Tool:** MySQL Workbench
- **Query Language:** SQL

## 🗄️ Database Structure

**Database Name:** `cinema_booking`

The project consists of seven tables.

| Table Name | Description |
|---|---|
| `movies` | Stores movie titles, genres, languages, duration, release dates, and ratings |
| `screens` | Stores cinema screen names, screen types, and seating capacity |
| `seats` | Stores seat numbers, row names, seat types, and screen references |
| `shows` | Stores show dates, timings, screen assignments, and ticket prices |
| `customers` | Stores customer details and registration dates |
| `bookings` | Stores booking information, total amounts, booking status, and payment details |
| `booking_seats` | Connects bookings with selected seats and shows, including seat prices |

## 🔗 Entity Relationship Diagram

The ER diagram represents the relationships between the seven database tables using primary keys (PK), foreign keys (FK), and relationship cardinalities.

Main relationships include:

- One movie can have multiple shows.
- One screen can host multiple shows.
- One screen can contain multiple seats.
- One customer can make multiple bookings.
- One show can have multiple bookings.
- Each booking can contain multiple booked seats.
- The `booking_seats` table connects bookings, shows, and seats.

**ER Diagram:** Add the project's ER diagram image to the repository and link it here.

Example image path:

`images/er-diagram.png`

![Cinema Seat and Ticket Booking System ER Diagram](images/er-diagram.png)

## ✨ Key Features

- Movie information management.
- Cinema screen and seat management.
- Show scheduling and ticket price management.
- Customer registration and booking records.
- Seat allocation and duplicate-booking prevention.
- Booking and payment status tracking.
- Automatic booking total calculation when seats are inserted.
- Show occupancy and customer spending reports.
- Revenue analysis by payment method.
- Available-seat retrieval for a particular show.
- Data integrity validation using SQL constraints and triggers.

## 💻 SQL Concepts Implemented

### 1. Database and Table Creation

- `CREATE DATABASE`
- `CREATE TABLE`
- Primary keys and foreign keys
- `AUTO_INCREMENT`
- `NOT NULL` and `UNIQUE` constraints
- `CHECK` constraints
- `ENUM` data types

### 2. Data Manipulation and Retrieval

- `INSERT`
- `SELECT`
- Filtering using `WHERE`
- Sorting using `ORDER BY`
- Joins between related tables
- Aggregate functions such as `COUNT()`, `SUM()`, and `AVG()`
- `GROUP BY` and `HAVING`
- Subqueries and `NOT EXISTS`

### 3. Indexes

The following indexes are created to support common searches:

- `idx_shows_date_time`
- `idx_shows_movie_date`
- `idx_bookings_customer_status`
- `idx_bookings_date`

### 4. Views

| View Name | Purpose |
|---|---|
| `view_show_schedule` | Displays movie schedules with screen information |
| `view_booking_details` | Combines booking, customer, movie, and payment details |
| `view_show_occupancy` | Calculates booked seats and occupancy percentage |
| `view_customer_booking_summary` | Summarizes confirmed bookings and customer spending |

### 5. Stored Procedures

| Procedure Name | Purpose |
|---|---|
| `sp_get_customer_bookings` | Retrieves bookings for a specified customer |
| `sp_revenue_by_payment` | Summarizes confirmed and successfully paid bookings by payment method |
| `sp_get_shows_by_date` | Retrieves shows scheduled on a specified date |
| `sp_get_available_seats` | Lists seats not assigned to non-cancelled bookings for a show |

### 6. Triggers

| Trigger Name | Purpose |
|---|---|
| `trg_validate_booking_show_insert` | Validates that a booked seat uses the same show as its booking |
| `trg_validate_seat_screen_insert` | Checks that a seat belongs to the screen assigned to the show |
| `trg_update_booking_total_insert` | Recalculates a booking's total after a seat is inserted |
| `trg_block_movie_delete` | Prevents deleting a movie while shows reference it |

### 7. Stored Functions

| Function Name | Purpose |
|---|---|
| `fn_booking_seat_total` | Calculates the total price of seats for a booking |
| `fn_customer_spending` | Calculates confirmed and successfully paid spending for a customer |
| `fn_available_seats` | Estimates remaining seats for a show using screen capacity and recorded seat assignments |

## 📊 Sample SQL Operations

### Display all movies

```sql
SELECT * FROM movies;
```

### Find movies with a rating above 8

```sql
SELECT title, genre, rating
FROM movies
WHERE rating > 8
ORDER BY rating DESC;
```

### Display movies with their show timings

```sql
SELECT m.title, sh.show_date,
       sh.start_time, sh.end_time,
       sh.ticket_price
FROM movies m
JOIN shows sh
    ON m.movie_id = sh.movie_id
ORDER BY sh.show_date, sh.start_time;
```

### Retrieve booking details

```sql
SELECT * FROM view_booking_details;
```

### Display show occupancy

```sql
SELECT * FROM view_show_occupancy;
```

### Retrieve bookings for a customer

```sql
CALL sp_get_customer_bookings(1);
```

### Generate revenue by payment method

```sql
CALL sp_revenue_by_payment();
```

### Calculate the total price of seats in a booking

```sql
SELECT fn_booking_seat_total(1)
AS booking_seat_total;
```

## 🚀 How to Run the Project

1. Install MySQL Server and MySQL Workbench.
2. Clone or download this repository.
3. Open MySQL Workbench and connect to your MySQL server.
4. Open the project's SQL script.
5. Execute the script from beginning to end.
6. Refresh the Schemas panel and open the `cinema_booking` database.
7. Inspect the tables, views, stored procedures, functions, triggers, and indexes.
8. Execute the sample SQL queries and stored procedure calls to view the results.

**Important:** The SQL script begins with `DROP DATABASE IF EXISTS cinema_booking;`. This deletes an existing database with that name before recreating it. Back up any important data before running the script.

## ✅ Data Integrity and Validation

The project uses primary keys, foreign keys, unique constraints, and check constraints to maintain data consistency.

It also includes triggers to validate booking-show relationships, ensure that selected seats belong to the correct screen, automatically recalculate booking totals after seat insertion, and prevent deleting movies referenced by shows.

Validation queries are included to check whether booked seats match their booking's show and the screen assigned to that show.

## 📁 Suggested Project Structure

```text
MySQL_Project/
│
├── README.md
├── cinema_booking.sql
└── images/
    └── er-diagram.png
```

*Use the actual SQL script filename and ER diagram filename present in your repository.*

## ⚠️ Limitations

- This project focuses on the database layer and does not include a front-end application or backend API in the supplied SQL script.
- The available-seat function estimates availability based on screen capacity and recorded seat assignments.
- The project uses sample records for demonstration and testing.
- The booking total trigger recalculates totals after seat insertion; other operations may require additional logic to keep totals synchronized.

## 🎓 Learning Outcomes

Through this project, I gained practical experience in:

- Relational database design and ER diagrams.
- Primary keys, foreign keys, and data integrity constraints.
- SQL joins, aggregate functions, and subqueries.
- Views, indexes, stored procedures, and stored functions.
- Trigger-based validation and automated calculations.
- Database reporting and query execution using MySQL Workbench.

## 🏁 Conclusion

The Cinema Seat & Ticket Booking System demonstrates how MySQL can be used to design and manage a relational database for cinema operations. It integrates database design, seat booking, payment tracking, data validation, and reporting into one project while providing practical experience with fundamental and advanced SQL concepts.

## 👨‍💻 Author

**Sai Lahar Cherukuri**

- GitHub Profile: [sailaharcherukuri](https://github.com/sailaharcherukuri)
