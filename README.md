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