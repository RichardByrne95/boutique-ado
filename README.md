# boutique-ado
A repository for the Boutique Ado project website.


## Development

### Project Setup

1.  A new repository called INSERT-NAME-HERE was created on GitHub.com.
2.  The repository was initialised with a 'README.md' and a .gitignore file. 
3.  The repository was cloned to the local machine by clicking 'Code', 'Open with GitHub Desktop' and then pressing 'Clone'.
4.  The project was opened in VS Code and a new terminal was created.
5.  Django was installed using the command: ```pip install django```
6.  A new Django project was created using the command ```django-admin startproject INSERT_NAME_HERE .```
7.  In order to prevent sensitive or unnecessary files being committed to GitHub, '*.sqlite3', '*.pyc' and '__pycache__' were added to the '.gitignore file.
8.  The project's status was verified by running the command ```python manage.py runserver```, and exposing PORT 8000.
9.  The initial Django migrations were run by typing ```python manage.py migrate``` into the command.
10. In order to log into Django's admin, a superuser was created using the command ```python manage.py createsuperuser``` and then providing a username, email and password.
11. The project was then committed to GitHub using the process in the Deployment section.

### Allauth Setup

In order to allow users to create an account, access their information, recover their account, verify that their account registration was successful and view personal order history, order confirmations and payment information, the Django Allauth package was installed to allow easy access to these functionalities.

1. To install All Auth, a new terminal was opened and the following command was typed: ```pip install django-allauth```.
2. From there, the request context processor was confirmed to be in 'settings.py'.
3. In order to ensure that all necessary code was in place before using Allauth, multiple code blocks were copied from [this link](https://django-allauth.readthedocs.io/en/latest/installation.html) and pasted into 'setting.py'. These included:
    -   The entire ```AUTHENTICATION_BACKENDS``` list.
    -   The following from ```INSTALLED_APPS```: ```django.contrib.sites```, ```allauth```, ```allauth.account```, ```allauth.socialaccount```.
    -   ```SITE_ID = 1``` was pasted beneath the ```AUTHENTICATION_BACKENDS``` list.
4. The changes made were migrated using the command ```python manage.py migrate```.
5. In order to facilitate social media authentication, the relevant code was added to the ```INSTALLED_APPS``` section. The domain name was also changed in the Django admin to SITENAME.example.com, and the display name was changed to SITENAME.
6. The Allauth templates were copied from Python's site-templates folder to our current project using the command ```xcopy C:\Users\USERNAME\AppData\Local\Programs\Python\Python39\Lib\site-packages\allauth\templates .templates\allauth /e```. This allows the templates to be customised to our liking.

### Creating an App in Django

Django apps were created using the following steps (APP_NAME is a placeholder name):

1.  A new terminal was opened and the following command was run: ```python manage.py startapp APP_NAME```
2.  A templates folder to hold the HTML was created inside the new app using the command: ```md APP_NAME/templates/APP_NAME```
3.  An 'index.html' file was created inside this second APP_NAME folder and extended the base template using: ```{% extends "base.html" %}```
4.  In order to render the new 'index.html' file, a new view was created in the 'views.py' file within the APP_NAME folder.
5.  The project-level 'urls.py' file was copied and pasted into the APP_NAME directory in order to provide a starting point for the APP_NAME app. A single empty path was added to indicate that this was the root url: ```path("", views.index, name='home')```.
6.  ```from . import views``` was used to import the views into this 'urls.py' file.
7.  Within the project level 'urls.py' file, the APP_NAME urls were added using the code: ```path('', include('home.urls'))```
8.  Lastly, the new APP_NAME app was added to ```INSTALLED_APPS``` in 'settings.py' and the following code was added to the ```DIRS``` list within ```TEMPLATES```: ```os.path.join(BASE_DIR, 'templates'), os.path.join(BASE_DIR, 'templates', 'allauth')```.

### Creating and Using Static Files

In order to use static files, like CSS and JavaScript files, the following steps were taken:

1.  A directory called 'static' was created in the main project directory.
2.  Sub-directories were created based on the different types of files that the project needed.
3.  The project's custom CSS file was linked using a ```<link>``` tag, and then using the Django template language to link to the custom CSS file.
4.  Within the project's 'settings.py' file, a tuple called ```STATICFILES_DIRS``` was created at the bottom of the file with a value of: ```(os.path.join(BASE_DIR, static'),)```
5.  In order to store the media files, two more variables were created beneath the ```STATICFILES_DIRS``` variable using the following code: ```MEDIA_URL = '/media/``` and ```MEDIA_ROOT = os.path.join(BASE_DIR, 'media')```
6. Lastly, for Django to see the MEDIA_URL, within main project's 'urls.py', two more modules were imported: ```from django.conf import settings
from django.conf.urls.static import static```
7. The MEDIA_URL was then appended to the ```urlpatterns``` list as demonstrated below:
```python
urlpatterns = [
    existing_path...
    existing_path...
    existing_path...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```