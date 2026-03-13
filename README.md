# JiMoney-Backend | A Personal Finance Management API

A robust RESTful API backend built with Flask and MySQL for managing personal finances, tracking multiple wallets, ledgers, and saving goals.

## 🚀 Tech Stack
* **Framework:** Python, Flask
* **Database:** MySQL (flask-mysqldb)
* **Environment:** python-dotenv
* **Testing:** Python `requests` library

## 📁 Project Architecture
This project utilizes Flask Blueprints to ensure a modular and scalable architecture:

* **`app.py`**: The main entry point that initializes the application, loads environment variables, synchronizes database states, and registers all blueprints.
* **`database.py`**: Handles the MySQL database connection instance.
* **`data.py`**: Core transaction module managing financial records (Datas). Includes strict SQL `COMMIT` and `ROLLBACK` mechanisms to ensure data integrity when updating related goals and ledgers concurrently.
* **`user.py`**: Manages user accounts, authentication, and personalized settings (e.g., UI dark mode, handedness, budgets).
* **`wallet.py`**: Provides CRUD operations for user wallets.
* **`ledger.py`**: Manages ledgers that belong to specific wallets.
* **`goal.py`**: Handles financial saving goals and tracks current accumulated amounts.
* **`test_app.py`**: Automated validation script to test various API endpoints.

## 🗄️ Database Schema
The database (`DBMS.sql`) is designed with relational integrity and cascade constraints:
* **Users**: Stores core user credentials and preferences.
* **Wallets**: A user can own multiple wallets.
* **Ledgers**: Each wallet can contain multiple ledgers.
* **Goals**: Financial targets associated with users.
* **Datas**: Represents individual transactions (income/expense).
* **Junction Tables (`DataToGoal`, `DataToLedger`)**: Resolves many-to-many relationships between transactions, goals, and ledgers.

## ⚙️ Setup & Installation

**1. Database Initialization**
Execute the provided SQL scripts in your MySQL environment:
* Run `DBMS.sql` to create the database schema and tables.
* (Optional) Run `Test_DBMS.sql` or `Test_wallet.sql` to insert mock data for testing.

**2. Environment Variables**
Create a `.env` file in the root directory to configure your MySQL connection:
```env
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
MYSQL_DB=DBMS
```

**3. Run the Server**
Start the Flask backend server on `0.0.0.0:5000`:
```bash
python app.py
```

**4. Run Tests**
Execute the automated test script to verify API endpoints:
```bash
python test_app.py
```