## Django Views & Templates

*manage.py is running django logic

- views in Django are similar to controllers in Express
    - they pass data to our templates

```bash
python manage.py shell_plus --ipython
```

## View Functions

1. import render into views.py

    render imports the views (first line)

    ```python
    from django.shortcuts import render
    from .models import Artist, Song
    # Create your views here.
    ```

2. create functions as views

    ```python
    # Create your views here.
    def artist_list(request):
        artists = Artist.objects.all()
    		return render(request, 'tunr/artist_list.html', {'artists': artists})
        # first argument is the kind of request
        # second argument is the actual view or template we want to show (like the path)
        # third argument is the information we want to pass (dictionary {'key': value})
    ```

## URLs

1. import "stuff" into urls.py

    ```python
    from django.conf.urls import include
    from django.urls import path
    from django.contrib import admin
    ```

2. "register" paths

    ```python
    # tunr_django/urls.py
    urlpatterns = [
        path('admin', admin.site.urls),
        path('', include('tunr.urls')),
    ]
    ```

3. create new "[urls.py](http://urls.py)" file in app folder (not app_django folder)
4. import "stuff" into new urls.py

    ```python
    from django.urls import path
    from . import views
    ```

5. create paths

    ```python
    urlpatterns = [
        # first argument is the path
        # second argument comes from view and is the function we are calling
        # third argument is parameter that is going to reference our templates in order to link one page from another
        path('', views.artist_list, name="artist_list"),
        path('songs/', views.song_list, name="song_list")
    ]
    ```

## Templates and Django Templating Language

- like handlebars
- this is the actual page that is being rendered when we go to the artist_list page (currently our landing page)
1. In the tunr directory, add a templates directory and a tunr subdirectory
2. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

3. In your browser, navigate to localhost:8000
- What's happening

## Artist Show

- now we need to add another route as a show page for each of the models
1. create a new function in tunr/views.py

    ```python
    # accepts the request and the parameter of pk so we can grab a specific artist
    def artist_detail(request, pk):
        artist = Artist.objects.get(id=pk)
        # all dictionaries are strings and need to be strings below
        return render(request, 'tunr/artist_detail.html', {'artist': artist})
    ```

2. create a new path in tunr/urls.py

    ```python
    # <int:pk> makes it dynamic in python
    path('artists/<int:pk>', views.artist_detail, name="artist_detail"),
    ```

3. create a template in the tunr/templates/tunr directory
4. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
5. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

## Artist Detail

- 
1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

Artist Detail

Add a back button

## Song Show

1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

Song Show

## Base HTML and CSS

- 
1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

base.html and CSS

## Artist Create

- 
1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

artist create

create form

edit views.py

edit urls.py

add a new template

## Artist Edit

- 
1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

artist edit

## Artist Delete

- 
1. create a new function
2. create a template
3. add new path to urls.py
    - make paths with slash so that paths don't interfere with each other
4. Here, create a file called artist_list.html and add the following code

    ```html
    <!-- tunr/templates/tunr/artist_list.html -->
    <h2>Artists <a href="">(+)</a></h2>
    <ul>
      {% for artist in artists %}
      <li>
        <a href="">{{ artist.name }}</a>
      </li>
      {% endfor %}
    </ul>
    ```

artist delete
