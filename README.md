---

##  Backend 


# Hope Connect Backend

## Powering a Platform for Positive Change

This repository contains the backend API for Hope Connect, a platform dedicated to facilitating donations, volunteer efforts, and community engagement for various charitable causes. This API provides the core logic, data management, and third-party integrations (like M-Pesa) that enable the frontend application to function.

---

---

## Features

* **User Authentication & Authorization:**
    * User registration and login (email/password).
    * JWT-based authentication.
    * Google Auth integration for seamless sign-up/login.
    * Role-based access control (e.g., `is_admin` for internal management).
* **Donation Management:**
    * API for creating, retrieving, and managing donations.
    * M-Pesa Integration integration for mobile money donations.
    
* **Volunteer Management:**
    * API for volunteer sign-up and profile management.
* **User Management:** CRUD operations for user profiles (e.g.,POST, GET).
* **Projectview:** Endpoints for creating, retrieving, and managing information about ongoing projects, campaigns, and impact stories.
* **Error Handling:** Centralized error handling for consistent API responses.

---

## Tech Stack

* **Backend Framework:** Flask
* **Database:** PostgreSQL
* **ORM:** Flask-SQLAlchemy
* **Database Migrations:** Flask-Migrate
* **Authentication:** Flask-JWT-Extended
* **Environment Variables:** python-dotenv
* **API Documentation:** [e.g.,(for Swagger UI generation) - *consider adding this if you plan for API docs*]
* **Payment Gateway:** M-Pesa Daraja API
* **Development Server:** Werkzeug (Flask's built-in)
* **Production WSGI Server:** Gunicorn

---

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

* Python 3.8+
* pip (Python package installer)
* PostgreSQL database server (running locally or accessible remotely)

---

## Installation

Follow these steps to set up the backend on your local machine:

1.  **Clone the repository:**
    ```bash
    git clone [your-backend-repo-url]
    cd [your-backend-repo-name]
    ```
   
    ```bash
    cd backend
    ```

2.  **Create and activate a virtual environment:**
    It's highly recommended to use a virtual environment to manage dependencies.

    ```bash
    python3 -m venv venv
    ```
    * **On macOS/Linux:**
        ```bash
        source venv/bin/activate
        ```
    
    You'll see `(venv)` in your terminal prompt when activated.

3.  **Install dependencies:**
    ```bash
    pipenv install

    pipenv shell
    
    ```
4.  **Set up environment variables:**
    Create `.env` and `.flaskenv` files in the `backend/` root directory.

    ```bash
    touch .env
    touch .flaskenv
    ```

    * **Edit `.flaskenv`:**
        ```
        # .flaskenv
        FLASK_APP=run.py
        FLASK_ENV=development
        ```

    * **Edit `.env` (add your local development secrets and settings):**
        ```
        # .env (THIS FILE IS GIT-IGNORED!)
        DATABASE_URL=postgresql://your_db_user:your_db_password@localhost:5432/hopeconnect_dev
        SECRET_KEY=a_super_long_random_secret_key_for_flask_app # Generate a strong random string
        JWT_SECRET_KEY=another_strong_random_key_for_jwt_tokens # Generate another strong random string
        MPESA_CONSUMER_KEY=your_mpesa_sandbox_consumer_key
        MPESA_CONSUMER_SECRET=your_mpesa_sandbox_consumer_secret
        # Add any other API keys or sensitive data needed for local development (e.g., Google Auth client secret)
        ```
        **Important:** Replace placeholder values with your actual local development credentials. Ensure `SECRET_KEY` and `JWT_SECRET_KEY` are long, random, and unique.

---

## Database Setup & Migrations

Make sure your PostgreSQL database server is running and your `DATABASE_URL` in `.env` is correctly configured.

1.  **Initialize Flask-Migrate (first time setup only):**
    ```bash
    flask db init
    ```
    This creates the `migrations/` directory.

2.  **Create initial migration:**
    ```bash
    flask db migrate -m "Initial migration"
    ```
    This command generates a new migration script based on your `app/models/` definitions. Review the generated file in `migrations/versions/` to ensure it's correct.

3.  **Apply migrations to the database:**
    ```bash
    flask db upgrade
    ```
    This creates the tables in your database according to your models.

---

## Running the Application

To run the Flask development server:

```bash
python run.py

##Project Structure##
backend/
├── server
│   ├── controller/
│   │   ├── auth.py (Authentication blueprints/routes)
│   │   ├── donations.py (Donation blueprints/routes)
│   │   ├── volunteers.py (Volunteer blueprints/routes)
│   │   ├── users.py (User-related blueprints/routes)
│   │   ├── events.py (Project View/Events blueprints/routes)
│   │   └── __init__.py (Registers blueprints)
│   ├── models/
│   │   ├── user.py
│   │   ├── donation.py
│   │   ├── volunteer.py
│   │   ├── event.py
│   │   └── __init__.py (Imports models for Flask-SQLAlchemy)
│   ├── services/
│   │   ├── auth_service.py (JWT handling, Google token verification)
│   │   ├── mpesa_service.py (Mpesa integration logic)   
│   ├── config.py (Configuration settings for different environments)
│   ├── extensions.py (Initializes Flask extensions like SQLAlchemy, JWT)
│   ├── __init__.py (Creates and configures the Flask app)
├── migrations/ (for Flask-Migrate)
├── instance/ (ignored by Git, for sensitive configs like database URI)
│   └── config.py (e.g., development.py, production.py)
