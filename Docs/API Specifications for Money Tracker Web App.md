# API Specifications for Money Tracker Web App

## 1. Introduction

This document provides detailed specifications for the RESTful APIs of the Money Tracker Web App. These APIs will serve as the communication layer between the frontend application and the backend services, enabling all core functionalities such as user management, transaction tracking, budgeting, and reporting. The APIs are designed to be intuitive, consistent, and secure.

## 2. Base URL

All API requests will be prefixed with the following base URL:

`https://api.moneytracker.com/v1` (Example, actual URL will be determined upon deployment)

## 3. Authentication

All API endpoints, except for user registration and login, will require authentication. The application will use **JSON Web Tokens (JWT)** for stateless authentication. Upon successful login, the server will return a JWT, which the client must include in the `Authorization` header of subsequent requests as a Bearer token.

**Header Example:**
`Authorization: Bearer <your_jwt_token>`

## 4. Error Handling

API errors will be returned with appropriate HTTP status codes and a JSON response body containing an error message and, optionally, a more detailed error code.

**Example Error Response:**
```json
{
  "message": "Invalid credentials",
  "code": "AUTH_001"
}
```

## 5. API Endpoints

### 5.1. User Management

#### 5.1.1. Register User
*   **Endpoint:** `/users/register`
*   **Method:** `POST`
*   **Description:** Registers a new user account.
*   **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "securepassword123"
    }
    ```
*   **Response (Success - 201 Created):**
    ```json
    {
      "message": "User registered successfully",
      "user_id": "uuid-of-user"
    }
    ```
*   **Response (Error - 400 Bad Request):**
    ```json
    {
      "message": "Email already registered",
      "code": "USER_001"
    }
    ```

#### 5.1.2. Login User
*   **Endpoint:** `/users/login`
*   **Method:** `POST`
*   **Description:** Authenticates a user and returns a JWT.
*   **Request Body:**
    ```json
    {
      "email": "user@example.com",
      "password": "securepassword123"
    }
    ```
*   **Response (Success - 200 OK):**
    ```json
    {
      "message": "Login successful",
      "access_token": "your_jwt_token",
      "token_type": "bearer"
    }
    ```
*   **Response (Error - 401 Unauthorized):**
    ```json
    {
      "message": "Invalid credentials",
      "code": "AUTH_001"
    }
    ```

#### 5.1.3. Get User Profile
*   **Endpoint:** `/users/profile`
*   **Method:** `GET`
*   **Description:** Retrieves the authenticated user's profile information.
*   **Authentication:** Required
*   **Response (Success - 200 OK):**
    ```json
    {
      "user_id": "uuid-of-user",
      "email": "user@example.com",
      "currency": "USD",
      "created_at": "2025-07-30T10:00:00Z"
    }
    ```

#### 5.1.4. Update User Profile
*   **Endpoint:** `/users/profile`
*   **Method:** `PUT`
*   **Description:** Updates the authenticated user's profile information.
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "currency": "EUR"
    }
    ```
*   **Response (Success - 200 OK):**
    ```json
    {
      "message": "Profile updated successfully"
    }
    ```

### 5.2. Account Management

#### 5.2.1. Add Manual Account
*   **Endpoint:** `/accounts`
*   **Method:** `POST`
*   **Description:** Adds a new manual financial account for the user.
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "name": "My Savings Account",
      "type": "savings",
      "initial_balance": 5000.00
    }
    ```
*   **Response (Success - 201 Created):**
    ```json
    {
      "message": "Account added successfully",
      "account_id": "uuid-of-account"
    }
    ```

#### 5.2.2. Link Bank Account (via Financial Data Aggregator)
*   **Endpoint:** `/accounts/link`
*   **Method:** `POST`
*   **Description:** Initiates the process to link a bank account via a financial data aggregator (e.g., Plaid Link token).
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "public_token": "public-token-from-aggregator",
      "institution_id": "ins_12345"
    }
    ```
*   **Response (Success - 200 OK):**
    ```json
    {
      "message": "Bank account linking initiated",
      "linked_accounts": [
        {
          "account_id": "uuid-of-linked-account-1",
          "name": "Checking Account",
          "balance": 1234.56
        },
        {
          "account_id": "uuid-of-linked-account-2",
          "name": "Credit Card",
          "balance": -500.00
        }
      ]
    }
    ```

#### 5.2.3. Get All Accounts
*   **Endpoint:** `/accounts`
*   **Method:** `GET`
*   **Description:** Retrieves all financial accounts for the authenticated user.
*   **Authentication:** Required
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "account_id": "uuid-of-account-1",
        "name": "Main Checking",
        "type": "checking",
        "balance": 2500.75,
        "linked": true
      },
      {
        "account_id": "uuid-of-account-2",
        "name": "Savings",
        "type": "savings",
        "balance": 10000.00,
        "linked": false
      }
    ]
    ```

### 5.3. Transaction Management

#### 5.3.1. Add Transaction
*   **Endpoint:** `/transactions`
*   **Method:** `POST`
*   **Description:** Adds a new income or expense transaction.
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "account_id": "uuid-of-account",
      "type": "expense",
      "amount": 50.00,
      "category": "Groceries",
      "description": "Weekly grocery shopping",
      "date": "2025-07-30"
    }
    ```
*   **Response (Success - 201 Created):**
    ```json
    {
      "message": "Transaction added successfully",
      "transaction_id": "uuid-of-transaction"
    }
    ```

#### 5.3.2. Get All Transactions
*   **Endpoint:** `/transactions`
*   **Method:** `GET`
*   **Description:** Retrieves all transactions for the authenticated user, with optional filters.
*   **Authentication:** Required
*   **Query Parameters:**
    *   `start_date` (optional): Filter transactions from this date (YYYY-MM-DD).
    *   `end_date` (optional): Filter transactions up to this date (YYYY-MM-DD).
    *   `category` (optional): Filter by category name.
    *   `type` (optional): Filter by transaction type (`income` or `expense`).
    *   `account_id` (optional): Filter by specific account.
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "transaction_id": "uuid-of-transaction-1",
        "account_id": "uuid-of-account-1",
        "type": "expense",
        "amount": 35.50,
        "category": "Dining Out",
        "description": "Dinner with friends",
        "date": "2025-07-29"
      },
      {
        "transaction_id": "uuid-of-transaction-2",
        "account_id": "uuid-of-account-1",
        "type": "income",
        "amount": 2000.00,
        "category": "Salary",
        "description": "Monthly paycheck",
        "date": "2025-07-25"
      }
    ]
    ```

#### 5.3.3. Update Transaction
*   **Endpoint:** `/transactions/{transaction_id}`
*   **Method:** `PUT`
*   **Description:** Updates an existing transaction.
*   **Authentication:** Required
*   **Path Parameters:** `transaction_id`
*   **Request Body:** (Partial updates allowed)
    ```json
    {
      "category": "Restaurants",
      "description": "Dinner at new place"
    }
    ```
*   **Response (Success - 200 OK):**
    ```json
    {
      "message": "Transaction updated successfully"
    }
    ```

#### 5.3.4. Delete Transaction
*   **Endpoint:** `/transactions/{transaction_id}`
*   **Method:** `DELETE`
*   **Description:** Deletes a transaction.
*   **Authentication:** Required
*   **Path Parameters:** `transaction_id`
*   **Response (Success - 204 No Content):** (Empty response body)

### 5.4. Budget Management

#### 5.4.1. Create Budget
*   **Endpoint:** `/budgets`
*   **Method:** `POST`
*   **Description:** Creates a new budget for a category over a period.
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "category": "Groceries",
      "amount": 400.00,
      "period": "monthly",
      "start_date": "2025-08-01"
    }
    ```
*   **Response (Success - 201 Created):**
    ```json
    {
      "message": "Budget created successfully",
      "budget_id": "uuid-of-budget"
    }
    ```

#### 5.4.2. Get All Budgets
*   **Endpoint:** `/budgets`
*   **Method:** `GET`
*   **Description:** Retrieves all budgets for the authenticated user.
*   **Authentication:** Required
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "budget_id": "uuid-of-budget-1",
        "category": "Groceries",
        "amount": 400.00,
        "spent": 150.00,
        "remaining": 250.00,
        "period": "monthly",
        "start_date": "2025-08-01",
        "status": "on_track"
      }
    ]
    ```

### 5.5. Goal Management

#### 5.5.1. Create Goal
*   **Endpoint:** `/goals`
*   **Method:** `POST`
*   **Description:** Creates a new financial goal.
*   **Authentication:** Required
*   **Request Body:**
    ```json
    {
      "name": "House Down Payment",
      "target_amount": 50000.00,
      "current_amount": 5000.00,
      "target_date": "2028-12-31",
      "type": "savings"
    }
    ```
*   **Response (Success - 201 Created):**
    ```json
    {
      "message": "Goal created successfully",
      "goal_id": "uuid-of-goal"
    }
    ```

#### 5.5.2. Get All Goals
*   **Endpoint:** `/goals`
*   **Method:** `GET`
*   **Description:** Retrieves all financial goals for the authenticated user.
*   **Authentication:** Required
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "goal_id": "uuid-of-goal-1",
        "name": "Emergency Fund",
        "target_amount": 10000.00,
        "current_amount": 3000.00,
        "progress_percentage": 30,
        "target_date": "2026-06-30",
        "type": "savings"
      }
    ]
    ```

### 5.6. Reporting and Insights

#### 5.6.1. Get Spending Breakdown by Category
*   **Endpoint:** `/reports/spending-by-category`
*   **Method:** `GET`
*   **Description:** Retrieves spending breakdown by category for a given period.
*   **Authentication:** Required
*   **Query Parameters:**
    *   `start_date` (required): Start date for the report (YYYY-MM-DD).
    *   `end_date` (required): End date for the report (YYYY-MM-DD).
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "category": "Groceries",
        "amount": 300.50
      },
      {
        "category": "Dining Out",
        "amount": 150.00
      }
    ]
    ```

#### 5.6.2. Get Income vs. Expense Trend
*   **Endpoint:** `/reports/income-expense-trend`
*   **Method:** `GET`
*   **Description:** Retrieves monthly income and expense trends.
*   **Authentication:** Required
*   **Query Parameters:**
    *   `start_date` (required): Start date for the report (YYYY-MM-DD).
    *   `end_date` (required): End date for the report (YYYY-MM-DD).
*   **Response (Success - 200 OK):**
    ```json
    [
      {
        "month": "2025-05",
        "income": 4000.00,
        "expense": 3000.00
      },
      {
        "month": "2025-06",
        "income": 4200.00,
        "expense": 3100.00
      }
    ]
    ```

This API specification provides a comprehensive guide for the development of the backend services. It will be a living document, updated as new features are added or existing ones are modified.

