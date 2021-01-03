## Django Rest Framework with Token Authentication

[https://git.generalassemb.ly/sei-921/drf-token-auth](https://git.generalassemb.ly/sei-921/drf-token-auth)

- in pipfile maybe take away requires
- apps are like modules that we can create in a modular fashion (that way we can move them to other projects in the future
- -f means use the file to the right
- /usr/local/opt/postgres/bin/createuser -s postgres in terminal will create a superuser "postgres" on mac
- don't run migrations until after you've checked the database
    - its a common practice to make a custom user (instasham)
    - we're doing a condensed version
- basic authentication is dangerous
- every django app has users
    - we can overwrite and create a custom user model
    - we should always create a django project by creating a custom user
        - otherwise if we want to make changes we have to start from scratch
- logging in is a post request because we are sending data (login credentials)
- postman environments are clutch

Links:

[https://djoser.readthedocs.io/en/latest/getting_started.html](https://djoser.readthedocs.io/en/latest/getting_started.html)

1. make project

    ```python
    mkdir drf-books && cd drf-books
    ```

2. make gitignore env and Procfile
3. initialize on git
4. open vs code and and stuff into gitignore
5. create the virtual environment
6. install django and dependencies
7. initialize django project
8. configure secret key
9. create and register a django app
10. configure installed apps
11. configure cors middleware
12. congifure postgresql
13. create settings.sql
14. configure settings.sql
15. configure databases
16. configure env file
17. exit the virtual environment and reactivate the shell
18. run the server (its okay if it says unapplied migrations)
19. install djangorestframework
20. configure installed apps in settings
21. add rest framework list to settings.py
    1. basic authentication is dangerous
    2. session authentication is like a cookie(super easy, barely an inconvenience but kind of lets us down in apis)
    3. token authentication (since there is no state the server sends you back a string. its the developers job to capture that and make sure that it is in each header request)
        1. O Auth is a way to pass off the request to a third aprty identity and the user can log in there. if thats successful they will end me a piece of info that says you are good to go and some information about you (nothing sensitive). then i give my credentials and in turn they will send me credentials that lets me do stuff as you (not me but you as the user)
22. import include into [urls.py](http://urls.py) with new urlpatterns
23. create a custom user
24. add a serializers.p[y](http://serializer.py) file
25. configure [settings.py](http://settings.py) (inside django project)
26. run migrations
27. create a superuser in the terminal
28. create your app with models
29. add serializers
    1. create meta classes
    2. create virtual fields
30. configure views
31. create and configure urls.py
32. configure django_books/urls.py