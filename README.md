# Football Ticket Booking System - Database Design & SQL Queries

## Overview

This project is a simplified Football Ticket Booking System database designed to demonstrate database design concepts, entity relationships, and SQL query skills.

The system manages football fans, tournament matches, and ticket booking transactions.

---

## Database Schema

The database contains the following tables:

### 1. Users

Stores information about football fans and ticket managers.

| Column       | Description                    |
| ------------ | ------------------------------ |
| user_id      | Unique user identifier         |
| full_name    | User full name                 |
| email        | User email address             |
| role         | Football Fan or Ticket Manager |
| phone_number | Contact number                 |

### 2. Matches

Stores football match information.

| Column              | Description               |
| ------------------- | ------------------------- |
| match_id            | Unique match identifier   |
| fixture             | Competing teams           |
| tournament_category | League or tournament name |
| base_ticket_price   | Standard ticket price     |
| match_status        | Availability status       |

### 3. Bookings

Stores ticket booking transactions.

| Column         | Description               |
| -------------- | ------------------------- |
| booking_id     | Unique booking identifier |
| user_id        | References Users table    |
| match_id       | References Matches table  |
| seat_number    | Allocated seat            |
| payment_status | Booking payment status    |
| total_cost     | Total booking cost        |

---

## Relationships

### One-to-Many

* One User can have many Bookings.

### Many-to-One

* Many Bookings can belong to one Match.

### Logical One-to-One

* Each Booking record represents one User booking one Match seat.

---



## Table Creation

### Users Table

```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY,
    full_name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    role VARCHAR(20)
        CHECK (role IN ('Ticket Manager', 'Football Fan')),
    phone_number VARCHAR(20)
);
```

### Matches Table

```sql
CREATE TABLE Matches (
    match_id INT PRIMARY KEY,
    fixture VARCHAR(100),
    tournament_category VARCHAR(100),
    base_ticket_price DECIMAL(10,2)
        CHECK (base_ticket_price >= 0),
    match_status VARCHAR(20)
        CHECK (
            match_status IN (
                'Available',
                'Selling Fast',
                'Sold Out',
                'Postponed'
            )
        )
);
```

### Bookings Table

```sql
CREATE TABLE Bookings (
    booking_id INT PRIMARY KEY,

    user_id INT REFERENCES Users(user_id),

    match_id INT REFERENCES Matches(match_id),

    seat_number VARCHAR(20),

    payment_status VARCHAR(20)
        CHECK (
            payment_status IN (
                'Pending',
                'Confirmed',
                'Cancelled',
                'Refunded'
            )
        ),

    total_cost DECIMAL(10,2)
        CHECK (total_cost >= 0)
);
```

---

## Sample Data

The database includes sample data for:

* 4 Users
* 5 Matches
* 5 Bookings

---

## SQL Queries

### Query 1

Retrieve all available Champions League matches.

### Query 2

Search users whose names start with "Tanvir" or contain "Haque".

### Query 3

Display bookings with missing payment status using COALESCE.

### Query 4

Retrieve booking details with user and match information using INNER JOIN.

### Query 5

Display all users including users without bookings using LEFT JOIN.

### Query 6

Find bookings whose total cost is greater than the average booking cost.

### Query 7

Retrieve the top 2 most expensive matches while skipping the highest priced match.

---



## Theory Questions Covered

1. Foreign Key and Referential Integrity
2. Aggregate Functions and HAVING Clause
3. Primary Key Constraints
4. LEFT JOIN Behavior
5. Main Query vs Subquery

---

## Project Structure

```text
.
├── README.md
├── QUERY.sql

```

---

## Submission Links

### ERD Link

https://drive.google.com/file/d/1OIhl9vzAAelGUSOhvywU4Q-Yf_LxUTxq/view

### Github Repo Link


### Interview Video Link

Add your public interview video link here.

---

## Author

Dishan Rahman

