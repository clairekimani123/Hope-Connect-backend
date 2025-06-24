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
