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
11. The project was then committed to GitHub using the process outlined in the Deployment section.

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
2.  A templates folder to hold the HTML was created inside the new app using the command: ```md APP_NAME\templates\APP_NAME```
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

### Creating an App with Fixtures

When an app was created that required creating database models, the following steps were executed:

1.  The steps from the 'Creating an App in Django' section were executed.
2.  The models were created using classes inside the 'models.py' file of the relevant app. An example of a model layout is as follows:
``` python
# Creates a Category class that inherits from the models.Model class
class Category(models.Model):
    # Adds a name field with a max length of 245 alpha-numeric characters
    name = models.CharField(max_length=254)
    # Add a frontend-friendly name that isn't required.
    friendly_name = models.CharField(max_length=254, null=True, blank=True)

    # Defines the '__str__' function so that it returns the name of the category
    def __str__(self):
        return self.name

    # Returns the frontend-friendly name of the category
    def get_friendly_name(self):
        return self.friendly_name
```
3.  The relevant models were then registered within the app's 'admin.py' file by, first importing the model(s) using ````from .models import MODEL_NAME```, and then by typing ```admin.site.register(MODEL_NAME)```
4.  The fixtures were then loaded by inputting the command: ```python manage.py loaddata FIXTURE_FILE_NAME``` This was repeated for each fixture.


### Migrating Changes in Django to the Database

When changes were made to models within a Django app, these changes were have to be 'migrated' to the database being used to have an effect for the end user. This was done using the following steps:

1.  A test run of the migrations was run using the command: ```python manage.py makemigrations --dry-run```
2.  To check that there aren't any issues with the models that are being migrated, the following command was run: ```python manage.py migrate -- plan```
3. When no issues were observed, the changes were migrated with the following command: ```python manage.py makemigrations``` followed by ```python manage.py migrate```

### Customising the Django Admin

Django's admin pages can be altered to correct things such as spelling mistakes or changing a record's visible name. These were done using the following steps:

1.  If a Django admin had not been set up, a superuser was created using the command ```python manage.py createsuperuser``` and then providing a username, email and password.
2.  Logged into Django's admin by running the command ```python manage.py runserver```, opening the exposed port in a brower, adding '/admin' to the end of the URL, and inputting admin credentials. From here, you can verify any error and changes you wish to make.
3.  To adjust the visible name of a group of models, a Meta class was added within the relevant model in the 'models.py' class using the following code: 
``` python
class Meta:
    verbose_name_plural = 'DISPLAY_NAME'
```
It's important to note that because the model itself is not being changed, this won't require migration.
4.  To change the fields of a model that are displayed in the admin, within the app's 'admin.py' file, add and customise the following code:
``` python
# Create a class that inherits the ModelAdmin class
class MODEL_NAMEAdmin(admin.ModelAdmin):
    # list_display is a tuple that will tell the admin which fields to display
    list_display = (
        'name of field to display...',
        'name of field to display...',
        'name of field to display...',
        'name of field to display...'
    )

    # Orders the records by chosen field (must be a tuple with a comma)
    ordering = ('FIELD_NAME',)
```
5.  Lastly, the MODEL_NAMEAdmin was registered along with the model itself using the following code:
``` python
admin.site.register(MODEL_NAME, MODELNAMEAdmin)
```

### Setting Up Search Functionality

In order for the user to be able to perform search queries on the site, the following steps were executed:

1.  A form element was set up in the relevant HTML page with a method of 'GET' and an action of "{% url 'VIEW_NAME' %}".
2.  An input element with a type of text and a name of 'q' (for query) was added inside the form.
3.  Within the 'views.py' file that contains the view referenced in the form element, the following code was added:
``` python
from django.db.models import Q
from django.shortcuts import redirect, reverse
from .models import Item_model_name

items_of_interest = Item_model_name.objects.all()
query = None

if request.GET:
        if 'q' in request.GET:
            query = request.GET['q']
            if not query:
                messages.error(request, "You didn't enter any dear criteria!")
                return redirect(reverse('products'))

            queries = Q(name__icontains=query) | Q(description__icontains=query)
            items_of_interest = items_of_interest.filter(queries)

context = {
    'items_of_interest': items_of_interest,
    'search_term': query
}
```








Kaggle.com was used as the source for the fixtures used.