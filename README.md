
customer-profile-service(Django)
=================================

Overview
--------
This is a Customer Management System built with Django. It provides basic CRM features: customers, products, orders, user authentication (admin and customer roles), and password reset via email.

Key Features
------------
- User registration, login, logout
- Admin dashboard with orders and customer management
- Customer user view and account settings (profile picture upload)
- Create / update / delete orders (including bulk order creation via inline formset)
- Product listing and tagging
- Password reset email flow

Tech stack
----------
- Python + Django (see `requirments.txt`)
- PostgreSQL for the database
- django-filter for filtering orders

Requirements
------------
- Python 3.8+
- PostgreSQL
- See `requirments.txt` for Python package versions

Quickstart (development)
-------------------------
1. Clone the repo

```bash
git clone <repo-url>
cd Customer-Management-System
```

2. Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

3. Install dependencies

```bash
pip install -r requirments.txt
```

4. Configure environment

Copy the example settings or set environment variables for secrets and DB credentials. The project currently stores defaults in `crm1/settings.py`; move these into environment variables for production. Common variables to set:

- `DJANGO_SECRET_KEY` (or replace `SECRET_KEY` in `crm1/settings.py`)
- `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT` (Postgres)
- `EMAIL_HOST_USER`, `EMAIL_HOST_PASSWORD` (for password reset emails)

5. Initialize the database

```bash
python manage.py migrate
python manage.py createsuperuser
```

6. Collect static files (optional for production)

```bash
python manage.py collectstatic
```

7. Run the development server

```bash
python manage.py runserver
```

Database
--------
The default DB configuration in `crm1/settings.py` points to PostgreSQL with the database name `DEMO_TEST`. Update these credentials or switch to SQLite for quick local experiments.

Media and static files
----------------------
- Static files live under the `static/` directory.
- Uploaded media (profile pictures) are stored under `static/images` as configured by `MEDIA_ROOT` in `crm1/settings.py`.

Routes (not exhaustive)
-----------------------
- `/` — admin dashboard (login required)
- `/register/` — user registration
- `/login/` — login
- `/logout/` — logout
- `/user/` — customer user page
- `/account/` — account settings
- `/products/` — product listing
- `/customer/<id>/` — customer detail and orders
- `/create_order/<id>/`, `/update_order/<id>/`, `/delete_order/<id>/` — order management
- Password reset flow: `/reset_password/`, `/reset_password_sent/`, `/reset/<uidb64>/<token>/`, `/reset_password_complete/`

Project structure
-----------------
- `accounts/` — main app: models, views, forms, templates, and URL routes
- `crm1/` — Django project settings and WSGI/ASGI
- `static/` — CSS and images
- `requirments.txt` — Python dependencies (note: filename is misspelled in repo)

Notes & Security
----------------
- `SECRET_KEY` and email/DB credentials are present in `crm1/settings.py`. Do not keep secrets in version control — use environment variables or a secrets manager.
- `DEBUG` is set to `True` in current settings; ensure it is disabled in production.

Contributing
------------
Feel free to open issues or pull requests. For substantial changes, open an issue first to discuss the approach.
