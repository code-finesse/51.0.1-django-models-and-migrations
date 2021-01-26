# Django Models and Migrations

- pip file is like package.json
- django is a package and a framework that helps to import info

<details>
<summary>Setup Django Application and Virtual Environment</summary>

1. make a new django directory and navigate into it

    ```python
    # in terminal
    mkdir tunr_django
    cd tunr_django
    ```

2. build the virtual environment by installing the pipenv (if not already installed)

    ```python
    # in terminal
    brew install pipenv
    ```

3. activate our virtual environment

    ```python
    # in terminal
    pipenv shell
    ```

4. make sure that the "Pipfile" looks similar to this

    ```python
    [[source]]
    name = "pypi"
    url = "https://pypi.org/simple"
    verify_ssl = true

    [dev-packages]

    [packages]
    django = "*"
    psycopg2-binary = "*"

    [requires]
    python_version = "3.7"
    ```

5. install django inside your newly created directory

    ```python
    pipenv install django
    ```

6. install the library for connecting django to PostrgreSQL

    ```python
    # in terminal
    pipenv install psycopg2-binary
    ```

7. start our django project

    ```python
    # in terminal
    pipenv run django-admin startproject tunr_django .
    ```

    - make sure that the . is at the end
    - what does this code do?
        - `django-admin` is the command line interface for interacting with Django. It has a few commands, of which `startproject` is the one to start a new Django project.
        - `tunr_django` is the name of our project. We add `.` after it so that the project is created in the current directory (the default is to create a new Django project in a new director).
        - `pipenv run` is required because we want to use the version of Django that we just installed using pipenv. If we leave off this part of the command, we'll use the version of the Django CLI that is installed globally (if there is one).
8. create our app with the name that will be after the "startapp"

    ```python
    django-admin startapp tunr
    ```

    - This step creates an "app" inside of our project repo called `tunr`. `tunr_django` is the base django project, where we handle our routes. `tunr` is where we write our models, controllers, and templates.
    - We can have many "apps" inside of a django project. This allows us to modularize our code, giving us flexibility and separation of concerns and making our code self-contained.
9. in the "tunr/settings.py" file find the INSTALLED_APPS constant dictionary and add "tunr" at the end

    *the name of the file may be different depending on the app name

    *this step is required to make things work

    ```python
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'tunr'
    ]
    ```

10. run brew services list to ensure that postgresql is running in terminal

    if it doesn't work you can run

    ```python
    # in terminal
    brew services restart postgresql
    ```

11. create settings.sql file in root directory and edit the database, users, and priveleges

    ```python
    # in terminal
    touch settings.sql

    # sttings.sql
    CREATE DATABASE tunr;
    CREATE USER tunruser WITH PASSWORD 'tunr';
    GRANT ALL PRIVILEGES ON DATABASE tunr TO tunruser;
    ```

12. run the following command from the root directory

    ```python
    psql -U postgres -f settings.sql
    ```

13. connect our app to the database by going to our "tunr_django/settings.py" file and making the DATABASES constant dictionary look like this

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'tunr',
            'USER': 'tunruser',
            'PASSWORD': 'tunr',
            'HOST': 'localhost'
        }
    }
    ```

14. run the server

    ```python
    python3 manage.py runserver
    ```

15. navigate to [localhost:8000](http://localhost:8000) to see the welcome page



</details>
<details>
<summary>What is the virtual environment?</summary>

The whole reason we need a virtual environment is that our computers have multiple versions of Python

Macs run Python2 for some background processes

But we code with Python3

So when we run a Django app, we need to create an isolated virtual environment, like a bubble, where there is only one specific version of Python … Python3

And all the Python dependencies like Django and PsycoPG, get installed to that virtual environment

</details>

## Models

- models file was auto generated when we created our app
- models.Model is the class we're extending from the models we are importing

```python
# we can create classes here as models
    # artist will be a table
    # anything in the artist class will be columns in our database

class Artist(models.Model):
    name = models.CharField(max_length=100)
    nationality = models.CharField(max_length=100)
    photo_url = models.TextField()

    # purpose of this dunder string is to return a string that users can understand
    def __str__(self):
        return self.name
```

## Migrations

- a migration is a set of changes/modifications intended for a database
    1. shut down the server and then run logic for migration changes

        ```python
        # in terminal

        $ python3 manage.py makemigrations 
        # (generated a migration file ("tunr/migrations/0001_initial.py")that got its data from models.py)
        # sets up the migration

        $ python3 manage.py migrate
        # (connected and put the tables inside of tunr database in postrgres)
        #actually performs the migration
        ```

    2. check database to ensure database was seeded

        ```python
        # in terminal
        $ psql "name of database"

        $ \dt
        ```

        * don't ever touch [initial.py](http://initial.py/) (if something is wrong just delete it and rerun it)

        *new files will autopopulate in "__**[init**.py](http://init.py)__" after migrations

## Foreign Keys

- we can make our classes with one to many relationships

```python
class Song(models.Model):
	    artist = models.ForeignKey(Artist, on_delete=models.CASCADE, related_name="songs")
    # this knows it needs to talk to some foreign key from the arguments we pass in
    # first argument is the relation
    # second argument is what happens when the parent is deleted (if we delete Kanye all of his songs will also be deleted)
    # third argument refers to how the model will be referred to in relation to its parent
```

## Admin Console

- superusers have authentication right out of the box so we don't have to write certain permissions
1. in the terminal run:

    ```python
    python3 manage.py createsuperuser
    ```

2. create the user by inputting a username, email, and password
3. in "tunr/admin.py" add the following code
    - any new models will need to be registered in this file

    ```python
    from django.contrib import admin
    from .models import Artist

    # Register your models here
    admin.site.register(Artist)
    ```

4. run the server and navigate to [localhost:8000/admin](http://localhost:8000/admin) to login
5. admire the full CRUD functionality for the model you created

## Django Extensions

- Django Extensions add additional debugging functionality to Django making coding easi
1. install through terminal

    ```python
    # in terminal
    pipenv install django-extensions
    ```

2. add django_extensions to your INSTALLED_APPS list:

    ```python
    # tunr_django/settings.py

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'tunr',
        'django_extensions'
    ]
    ```

3. install ipython for a nicer interface

    ```python
    # in terminal
    pipenv install ipython
    ```

4. run it

    ```python
    # in terminal
    python3 manage.py shell_plus --ipython
    ```

5. this allows us to use many common features that django provides without having to import them ourselves

    ```python

    ```

## Django's ORM

- Django has an ORM, similar to Mongoose in Express
- this is the shell we will use

```python
# Select all of the artist objects in the database
Artist.objects.all()

# Select All Objects and Print All Values
Artist.objects.all().values_list()

# Select All Objects and Print Specific Value
Artist.objects.all().values_list('nationality')

# Get the artist with the id of 1 (can also do pk here which stands for primary key)
Artist.objects.get(id=1)

# Get the artist with the name "Kanye West", if there are two Kanye's this will error!
Artist.objects.get(name="Kanye West")

# Get all the Artists who are from the USA
Artist.objects.filter(nationality="USA")

# Store an artist in a variable for later access:
p = Artist.objects.get(name="Kanye West")

# Now you can look up the artist's songs:
p.songs.all()
p.songs.all().values_list()

# Create an Artist with the following attributes, then save, commiting it to the database
kanye = Artist(name="Kane West", photo_url="test.com", nationality="USA")
kanye.save()

# Oops, we misspelled Kanye's name! Let's change it and then commit to the DB
kanye.name = "Kanye West"
kanye.save()

# Let's add a song to the artist
song = Song(title="Ultralight Beam", album="The Life of Pablo", preview_url="test.com", artist=kanye)
song.save()

# Delete the song
song.delete()
```

- we can do more complex operations also

    [https://django-extensions.readthedocs.io/en/latest/shell_plus.html](https://django-extensions.readthedocs.io/en/latest/shell_plus.html)

    ```python
    # This will return all Artists who's name starts with an A
    Artist.objects.filter(name__startswith="A")

    # This will return all the songs with the id's 1 and 2, excluding all those equal to or greater than 3
    Song.objects.exclude(artist_id__gte=3)
    ```

*django does have a shell built in by default:

```python
# in terminal
python3 manage.py shell
```

*it can do everything we do in the shell_plus, but doesn't automatically import our models

if we wanted to import manually, we'd type this into the shell:

```python
from .models import Artist, Song

Artist.objects.all()
```

**TO SHUT DOWN A VIRTUAL ENVIRONMENT**:

Write

```
deactivate
```

right inside of the virtual env

That will give you a bash terminal back but it looks weird

Write

```
exit
```

to get the regular bash shell back
