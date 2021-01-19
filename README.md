# boutique-ado
A repository for the Boutique Ado project website.


## Development

### Project Setup

1.  A new repository called INSERT-NAME-HERE was created on GitHub.com.
2.  The repository was initialised with a README.md and a .gitignore file. 
3.  The repository was cloned to the local machine by clicking 'Code', 'Open with GitHub Desktop' and then pressing 'Clone'.
4.  The project was opened in VS Code and a new terminal was created.
5.  Django was installed using the command 'pip install django'.
6.  A new Django project was created using the command 'django-admin startproject INSERT_NAME_HERE .'.
7.  In order to prevent sensitive or unnecessary files being committed to GitHub, '*.sqlite3', '*.pyc' and '__pycache__' were added to the '.gitignore file.
8.  The project's status was verified by running the command 'python manage.py runserver', and exposing PORT 8000.
9.  The initial Django migrations were run by typing 'python manage.py migrate' into the command.
10. In order to log into Django's admin, a superuser was created using the command 'python manage.py createsuperuser' and then providing a username, email and password.
11. The project was then committed to GitHub using the process in the Deployment section.

### Allauth Setup

In order to allow users to create an account, access their information, recover their account, verify that their account registration was successful and view personal order history, order confirmations and payment information, the Django Allauth package was installed to allow easy access to these functionalities.

1. To install All Auth, a new terminal was opened and the following command was typed: 'pip install django-allauth'.
2. From there, the request context processor was confirmed to be in 'settings.py'.
3. In order to ensure that all necessary code was in place before using Allauth, multiple code blocks were copied from [this link](https://django-allauth.readthedocs.io/en/latest/installation.html) and pasted into 'setting,py'. These included:
    -   The entire 'AUTHENTICATION_BACKENDS' list.
    -   The following from 'INSTALLED_APPS': 'django.contrib.sites', 'allauth', 'allauth.account', 'allauth.socialaccount'.
    -   'SITE_ID = 1' was pasted beneath the 'AUTHENTICATION_BACKENDS' list.
4. The changes made were migrated using the command 'python manage.py migrate'.
5. In order to facilitate social media authentication, the relevant code was added to the 'INSTALLED_APPS' section. The domain name was also changed in the Django admin to SITENAME.example.com, and the display name was changed to SITENAME.
6. The Allauth templates were copied from Python's site-templates folder to our current project using the command 'xcopy C:\Users\Richard\AppData\Local\Programs\Python\Python39\Lib\site-packages\allauth\templates .templates\allauth /e'. This allows the templates to be customised to our liking.

### Creating an App in Django

Django apps were created using the following steps:

1.  A new terminal was opened and the following command was run: 'python manage.py startapp APP_NAME'
2.  A templates folder was created inside the new app using the command: 'md APP_NAME/templates/APP_NAME'
3.  An 'index.html' file was created inside this last home folder and extended the base template using: '{% extends "base.html" %}'
4.  The project-level 'urls.py' file was copied and pasted into the home app directory in order to provide a starting point for the home app.