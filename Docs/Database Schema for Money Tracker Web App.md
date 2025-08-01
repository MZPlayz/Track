# Database Schema for Money Tracker Web App

## 1. Introduction

This document details the database schema for the Money Tracker Web App. It defines the tables, their columns, data types, relationships, and constraints. The schema is designed to efficiently store and manage all application data, including user information, financial accounts, transactions, budgets, and goals.

## 2. Database System

**PostgreSQL** is the chosen relational database management system (RDBMS) due to its robustness, ACID compliance, extensibility, and strong support for complex queries and data integrity.

## 3. Table Definitions

### 3.1. `users` Table

Stores user authentication and profile information.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `user_id`      | `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the user            |
| `email`        | `VARCHAR(255)`      | `NOT NULL`, `UNIQUE`                      | User's email address (used for login)     |
| `password_hash`| `VARCHAR(255)`      | `NOT NULL`                                | Hashed password for security              |
| `currency`     | `VARCHAR(3)`        | `DEFAULT 'USD'`                           | Preferred currency (e.g., USD, EUR)       |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of user creation                |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

### 3.2. `accounts` Table

Stores details of financial accounts linked or manually added by users.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `account_id`   | `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the account         |
| `user_id`      | `UUID`              | `NOT NULL`, `FOREIGN KEY (users.user_id)` | Foreign key to the `users` table          |
| `name`         | `VARCHAR(255)`      | `NOT NULL`                                | User-defined name for the account         |
| `type`         | `VARCHAR(50)`       | `NOT NULL`                                | Type of account (e.g., 'checking', 'savings', 'credit_card', 'investment') |
| `current_balance`| `NUMERIC(15, 2)`    | `NOT NULL`                                | Current balance of the account            |
| `linked`       | `BOOLEAN`           | `NOT NULL`, `DEFAULT FALSE`               | True if linked to a financial institution, false if manual |
| `institution_name`| `VARCHAR(255)`      | `NULLABLE`                                | Name of the financial institution (if linked) |
| `external_id`  | `VARCHAR(255)`      | `UNIQUE`, `NULLABLE`                      | ID from financial data aggregator (if linked) |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of account creation             |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

### 3.3. `transactions` Table

Stores individual income and expense transactions.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `transaction_id`| `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the transaction     |
| `account_id`   | `UUID`              | `NOT NULL`, `FOREIGN KEY (accounts.account_id)` | Foreign key to the `accounts` table       |
| `user_id`      | `UUID`              | `NOT NULL`, `FOREIGN KEY (users.user_id)` | Foreign key to the `users` table (for direct user access) |
| `type`         | `VARCHAR(50)`       | `NOT NULL`                                | 'income' or 'expense'                     |
| `amount`       | `NUMERIC(15, 2)`    | `NOT NULL`                                | Amount of the transaction                 |
| `category_id`  | `UUID`              | `NOT NULL`, `FOREIGN KEY (categories.category_id)` | Foreign key to the `categories` table     |
| `description`  | `TEXT`              | `NULLABLE`                                | Description of the transaction            |
| `transaction_date`| `DATE`              | `NOT NULL`                                | Date of the transaction                   |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of transaction creation         |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

### 3.4. `categories` Table

Stores user-defined and system-defined transaction categories.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `category_id`  | `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the category        |
| `user_id`      | `UUID`              | `NULLABLE`, `FOREIGN KEY (users.user_id)` | Foreign key to `users` table (NULL for system categories) |
| `name`         | `VARCHAR(255)`      | `NOT NULL`                                | Name of the category (e.g., 'Groceries', 'Rent') |
| `type`         | `VARCHAR(50)`       | `NOT NULL`                                | 'income' or 'expense'                     |
| `is_custom`    | `BOOLEAN`           | `NOT NULL`, `DEFAULT FALSE`               | True if user-defined, false if system-defined |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of category creation            |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

### 3.5. `budgets` Table

Stores budget configurations for categories over specific periods.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `budget_id`    | `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the budget          |
| `user_id`      | `UUID`              | `NOT NULL`, `FOREIGN KEY (users.user_id)` | Foreign key to the `users` table          |
| `category_id`  | `UUID`              | `NOT NULL`, `FOREIGN KEY (categories.category_id)` | Foreign key to the `categories` table     |
| `amount`       | `NUMERIC(15, 2)`    | `NOT NULL`                                | Budgeted amount for the period            |
| `period_type`  | `VARCHAR(50)`       | `NOT NULL`                                | 'monthly', 'weekly', 'yearly', etc.       |
| `start_date`   | `DATE`              | `NOT NULL`                                | Start date of the budget period           |
| `end_date`     | `DATE`              | `NOT NULL`                                | End date of the budget period             |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of budget creation              |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

### 3.6. `goals` Table

Stores financial goals set by users.

| Column Name    | Data Type           | Constraints                               | Description                               |
| :------------- | :------------------ | :---------------------------------------- | :---------------------------------------- |
| `goal_id`      | `UUID`              | `PRIMARY KEY`, `DEFAULT gen_random_uuid()` | Unique identifier for the goal            |
| `user_id`      | `UUID`              | `NOT NULL`, `FOREIGN KEY (users.user_id)` | Foreign key to the `users` table          |
| `name`         | `VARCHAR(255)`      | `NOT NULL`                                | Name of the financial goal                |
| `target_amount`| `NUMERIC(15, 2)`    | `NOT NULL`                                | Target amount to achieve                  |
| `current_amount`| `NUMERIC(15, 2)`    | `NOT NULL`, `DEFAULT 0.00`                | Current amount saved/contributed          |
| `target_date`  | `DATE`              | `NULLABLE`                                | Target date for achieving the goal        |
| `type`         | `VARCHAR(50)`       | `NOT NULL`                                | Type of goal (e.g., 'savings', 'debt_repayment') |
| `is_achieved`  | `BOOLEAN`           | `NOT NULL`, `DEFAULT FALSE`               | True if the goal has been achieved        |
| `created_at`   | `TIMESTAMP WITH TIME ZONE` | `NOT NULL`, `DEFAULT NOW()`               | Timestamp of goal creation                |
| `updated_at`   | `TIMESTAMP WITH TIME ZONE` | `DEFAULT NOW()`                           | Last update timestamp                     |

## 4. Relationships

*   `users` ONE-TO-MANY `accounts`: One user can have multiple accounts.
*   `users` ONE-TO-MANY `transactions`: One user can have multiple transactions.
*   `users` ONE-TO-MANY `categories`: One user can have multiple custom categories.
*   `users` ONE-TO-MANY `budgets`: One user can have multiple budgets.
*   `users` ONE-TO-MANY `goals`: One user can have multiple goals.
*   `accounts` ONE-TO-MANY `transactions`: One account can have multiple transactions.
*   `categories` ONE-TO-MANY `transactions`: One category can be associated with multiple transactions.
*   `categories` ONE-TO-MANY `budgets`: One category can have multiple budgets (across different users/periods).

## 5. Indexes

Indexes will be created on frequently queried columns to optimize performance:
*   `users`: `email` (for login)
*   `accounts`: `user_id`
*   `transactions`: `account_id`, `user_id`, `category_id`, `transaction_date`
*   `budgets`: `user_id`, `category_id`, `start_date`
*   `goals`: `user_id`

## 6. Constraints

*   **Primary Keys:** Ensure unique identification for each record.
*   **Foreign Keys:** Maintain referential integrity between related tables.
*   **NOT NULL:** Ensure essential data is always present.
*   **UNIQUE:** Ensure uniqueness for columns like `email` and `external_id`.
*   **Data Type Constraints:** Ensure data conforms to expected types and ranges (e.g., `NUMERIC(15, 2)` for amounts).

This database schema provides a structured and efficient way to store the Money Tracker Web App's data, supporting all defined functional requirements.

