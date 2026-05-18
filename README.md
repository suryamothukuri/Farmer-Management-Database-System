# Farmer Management System

A Flask-based web application for managing farmer records, farming categories, agro-product listings, and database activity logs. The project provides authentication, farmer registration, product management, and trigger-based audit tracking using a MySQL database.

## Project Overview

The Farmer Management System is designed to maintain farmer information and related agricultural product details through a simple web interface. Authenticated users can register farmers, update existing farmer records, delete records, add farming categories, and manage agro-product listings. The system also includes MySQL triggers to automatically track insert, update, and delete operations performed on farmer records.

## Features

- User signup and login authentication
- Password hashing using Werkzeug security utilities
- Farmer registration with details such as name, Aadhaar number, age, gender, phone number, address, and farming type
- View all registered farmer details
- Edit and delete farmer records
- Add and manage farming categories
- Add and view agro-products with product name, description, price, username, and email
- Trigger-based activity tracking for farmer insert, update, and delete operations
- Flash messages for user feedback
- MySQL database integration using Flask-SQLAlchemy
- Responsive frontend using HTML, CSS, Bootstrap, JavaScript, and Jinja templates

## Tech Stack

### Backend

- Python
- Flask
- Flask-SQLAlchemy
- Flask-Login
- Werkzeug Security

### Database

- MySQL / MariaDB
- SQL triggers
- phpMyAdmin-compatible SQL dump

### Frontend

- HTML
- CSS
- Bootstrap
- JavaScript
- Jinja2 Templates

## Folder Structure

```text
farmer system/
├── main.py
├── farmers.sql
├── templates/
│   ├── index.html
│   ├── base.html
│   ├── auth.html
│   ├── login.html
│   ├── signup.html
│   ├── farmer.html
│   ├── farmerdetails.html
│   ├── edit.html
│   ├── farming.html
│   ├── agroproducts.html
│   ├── addagroproducts.html
│   └── triggers.html
└── static/
    ├── css/
    ├── images/
    └── assets/
        ├── css/
        ├── js/
        └── vendor/
```

## Database Design

The project uses a MySQL database named `farmers`.

### Main Tables

| Table | Purpose |
|---|---|
| `user` | Stores registered application users with hashed passwords |
| `register` | Stores farmer registration details |
| `farming` | Stores farming type/category information |
| `addagroproducts` | Stores agro-product listing details |
| `trig` | Stores trigger-generated activity logs |
| `test` | Used to verify database connectivity |

### Database Triggers

The SQL file includes triggers on the `register` table:

| Trigger | Event | Purpose |
|---|---|---|
| `insertion` | After insert | Logs when a farmer record is inserted |
| `updation` | After update | Logs when a farmer record is updated |
| `deletion` | Before delete | Logs when a farmer record is deleted |

These logs are stored in the `trig` table and can be viewed from the application.

## Application Routes

| Route | Description | Access |
|---|---|---|
| `/` | Home page | Public |
| `/signup` | User registration | Public |
| `/login` | User login | Public |
| `/logout` | Logout current user | Authenticated |
| `/register` | Register farmer details | Authenticated |
| `/farmerdetails` | View farmer records | Authenticated |
| `/edit/<rid>` | Edit farmer record | Authenticated |
| `/delete/<rid>` | Delete farmer record | Authenticated |
| `/addfarming` | Add farming type | Authenticated |
| `/addagroproduct` | Add agro-product | Authenticated |
| `/agroproducts` | View agro-products | Public |
| `/triggers` | View database trigger logs | Authenticated |
| `/test` | Test database connection | Public |

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```

Replace `your-username` and `your-repository-name` with your actual GitHub username and repository name.

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate the virtual environment:

For macOS/Linux:

```bash
source venv/bin/activate
```

For Windows:

```bash
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install Flask Flask-SQLAlchemy Flask-Login Werkzeug mysqlclient
```

If `mysqlclient` causes installation issues, use PyMySQL instead:

```bash
pip install pymysql
```

Then update the database connection accordingly in `main.py` if needed.

### 4. Set Up the MySQL Database

Create a MySQL database named:

```sql
CREATE DATABASE farmers;
```

Import the provided SQL file:

```bash
mysql -u root -p farmers < farmers.sql
```

You can also import `farmers.sql` using phpMyAdmin.

### 5. Configure Database Connection

In `main.py`, update the database URI if your MySQL username, password, host, or database name is different:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:@localhost/farmers'
```

Example with password:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:yourpassword@localhost/farmers'
```

### 6. Run the Application

```bash
python main.py
```

The application will start locally at:

```text
http://127.0.0.1:5000/
```

## Key Implementation Details

- Flask handles routing and request processing.
- Flask-Login manages user sessions and protected routes.
- Werkzeug hashes user passwords before storing them in the database.
- Flask-SQLAlchemy defines database models and connects the application to MySQL.
- Jinja2 templates render dynamic HTML pages.
- MySQL triggers provide automatic audit logging for farmer record changes.

## Notes

- The current database URI is configured for a local MySQL setup using the `root` user and no password.
- Update the database credentials before running the project on another machine.
- Do not expose real database credentials or secret keys in a public repository.
- For production deployment, store the secret key and database URL in environment variables.
