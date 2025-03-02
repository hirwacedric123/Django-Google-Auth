# AllAuth Google Login Project

A Django web application that demonstrates authentication with Google using django-allauth. This project provides a simple implementation of third-party authentication, focusing on Google OAuth integration.

## Features

- User authentication with Google accounts
- Custom user authentication flow
- Simple Django templates for login/signup interfaces
- SQLite database for development

## Project Structure

```
AllAuthProj/
├── AllAuthApp/        # Main application directory
├── AllAuthProj/       # Project settings directory
├── templates/         # HTML templates
├── authenv/           # Virtual environment (not tracked in git)
├── .gitignore         # Git ignore file
├── db.sqlite3         # SQLite database
├── manage.py          # Django management script
└── README.md          # This file
```

## Prerequisites

- Python 3.8+
- Django 3.2+
- A Google Cloud Platform account with OAuth credentials

## Installation

1. Clone the repository:
```bash
git clone https://github.com/hirwacedric123/Django-Google-Auth.git
cd AllAuthProj
```

2. Create and activate a virtual environment:
```bash
python -m venv authenv
source authenv/bin/activate  # On Windows: authenv\Scripts\activate
```

3. Install the required packages:
```bash
pip install -r requirements.txt
```

4. Set up your Google OAuth credentials:
   - Go to the [Google Developer Console](https://console.developers.google.com/)
   - Create a new project
   - Enable the Google+ API
   - Create OAuth credentials (Web application type)
   - Add your domain to the authorized domains
   - Set redirect URIs (typically: http://localhost:8000/accounts/google/login/callback/)
   - Copy your Client ID and Client Secret

5. Configure your Django settings:
   - Add your Google OAuth credentials in the Django admin interface or settings.py

## Configuration

In your `settings.py` file, ensure you have the following configurations:

```python
INSTALLED_APPS = [
    # ...
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
    # ...
]

MIDDLEWARE = [
    # ...
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    # ...
]

AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
]

SITE_ID = 1

# Provider specific settings
SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'APP': {
            'client_id': 'YOUR_CLIENT_ID',
            'secret': 'YOUR_CLIENT_SECRET',
            'key': ''
        }
    }
}

LOGIN_REDIRECT_URL = '/'
```

## Running the Application

1. Apply migrations:
```bash
python manage.py migrate
```

2. Create a superuser:
```bash
python manage.py createsuperuser
```

3. Run the development server:
```bash
python manage.py runserver
```

4. Access the application at http://localhost:8000

## Usage

1. Navigate to the login page
2. Click on the "Sign in with Google" button
3. Authorize the application in the Google OAuth consent screen
4. You will be redirected back to your application, now logged in with your Google account

## Customization

You can customize the authentication flow and templates:

- Edit templates in the `templates` directory
- Modify authentication logic in the views
- Extend the user model if needed

## License

[Add your preferred license here]

## Acknowledgments

- [Django documentation](https://docs.djangoproject.com/)
- [django-allauth documentation](https://django-allauth.readthedocs.io/)
- [Google OAuth documentation](https://developers.google.com/identity/protocols/oauth2)
