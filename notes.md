# Intorduction

- Python based web framework
- Django is based on MVT(MOdel-View-Template)

# Building Blocks of Django

* Models :
- define the structure of your data and how it interacts with the database.
- Create models to represent your data entities, using Django's ORM to handle database queries.

* Views :
- handle the business logic and return HTTP responses.
- Write views to process requests, interact with models, and render templates.

* Templates :
- HTML files that define the presentation layer of your application, allowing for dynamic content.

- Use Django’s templating engine to create reusable and dynamic HTML views.

* URLs :
- URL routing that maps URLs to views.

* Forms :
- handle form validation and data processing.
- Use Django forms to create and process HTML forms easily, including validation and error handling.

* Admin Interface :
-  built-in administrative interface for managing your models.
- Customize the admin panel to manage your application’s data effortlessly.

* Middleware :
- Layers of processing that can be applied to requests and responses.
- Use middleware for tasks like authentication, logging, or modifying requests and responses.

* Authentication & Authorization :
- Built-in features for managing user accounts and permissions.
-  Implement user authentication, permissions, and groups to control access to various parts of your application.


# pip list and pip freezeee

* pip list : 

- This command provides a human-readable list of installed packages in the current environment.
- Useful for quickly checking what packages are installed and their versions.

Package        Version
-------------- -------
Django         4.1.2
requests       2.26.0

* pip freeze :

- This command generates output suitable for creating a requirements.txt file, which can be used to replicate the environment later.

- Best used when you need to capture the exact versions of packages for dependency management or deployment.

Django==4.1.2
requests==2.26.0


# MVT DESIGN PATTERN

* Model : provides the interface for data stored in the db.
- It defines the structure of your database tables and contains the business logic.

- Responsibilities:
Interact with the database (create, read, update, delete data).
Define relationships between different data entities.
Include methods to handle data processing.





* Views : serves as bridge between model data and templates.

- It processes user requests, interacts with the Model to fetch or manipulate data, and sends the appropriate response.

- Responsibilities:
Handle user input and HTTP requests.
Retrieve data from the Model.
Select and return the appropriate Template for rendering.



* Templates : responsible for entire user interface.

- data is presented to the user, typically using HTML.

- Responsibilities:
Render data provided by the View into a user-friendly format.
Use Django's templating language to include dynamic content, loops, and conditional logic.


# How MVT Works Together 

1. User Request: A user sends a request (e.g., visiting a URL).

2. View Processing: Django routes the request to the appropriate View based on the URL configuration. The View processes the request.

3. Model Interaction: The View interacts with the Model to retrieve or manipulate data.

4. Template Rendering: The View prepares data and selects a Template to render the response.

5. Response to User: The Template generates HTML that is sent back to the user's browser.


# Create Django Project BoilerPlate

* django-admin startapp projecy_name

* Create View in views.py

    def Home(req):
    return HttpResponse("<h1>Hello</h1>")

* Create urls.py file in app folder

* Routing(url configuration)

    - add view into the urls.py

    urlpatterns = [
        path("Home", views.Home, name="Home")
    ]

* Connecting app folder urls file to project folder urls

    urlpatterns = [
        path("admin/", admin.site.urls),
        path("djangobasicapp/",include("djangobasicapp.urls"))
    ]

* Run the server
 
    python manage.py runserver
    (in url enter correct path i.e localhost/djangobasicapp/Home)


# HTTPs REQUEST

* GET: Retrieve data from the server.
* POST: Send data to the server to create a new resource.
* PUT: Update an existing resource with new data (typically replacing the entire resource).
* DELETE: Remove a resource from the server.
* PATCH:  Partially update an existing resource.
           allows you to update only the fields you specify, leaving all other fields unchanged.

# Django Project Structure

* Manage.py

- The manage.py file is a crucial part of any Django project, acting as a command-line utility for managing your application.
- This is a command-line utility that allows you to interact with your Django project. You can run the server, apply migrations, create apps, and more.
- It serves as a wrapper around django-admin and sets the environment for your project.

* Setting.py

- Contains all the configuration settings for your Django project, such as database configurations, installed apps, middleware, and static file settings.

* Urls.py

- This file defines the URL patterns for your project. It routes requests to the appropriate view based on the URL.

* asgi.py

- This file is for ASGI (Asynchronous Server Gateway Interface) applications. It’s useful for running Django with asynchronous frameworks.

* wsgi.py

- This file is for WSGI (Web Server Gateway Interface) applications, allowing your Django project to communicate with web servers. It’s the standard interface for Python web applications.


# Django App Folder Structre

* Migrations

- This directory contains migration files that Django uses to apply changes to your database schema.

* __init__.py

- An empty file that tells Python to treat the directory as a package. You can also use it to define package-level variables or imports.

* admin.py

- Register your models here to make them accessible in the Django admin interface.

* apps.py

- Contains configuration for the app. Here, you can set the app’s name and other metadata.

* models.py

- Define your data models (database schema) here. Each model is a Python class that corresponds to a database table.

* tests.py

- Write unit tests for your app here to ensure its functionality and reliability.

* views.py

- Define your view functions or class-based views that handle incoming requests and return responses.


# Request Life Cycle

1. HTTP Request:

A user interacts with a web browser and sends an HTTP request (e.g., GET, POST) to your Django application.

2. URL Routing:

The request reaches the Django server, which uses the urls.py files to match the incoming URL to a specific view.

Django checks each URL pattern defined in urls.py to find a match.

3. View Function:

Once a matching URL is found, Django calls the corresponding view function or class-based view.

The view receives the HTTP request and any parameters captured from the URL.

4. Middleware Processing:

Before the view is executed, any middleware specified in the MIDDLEWARE setting will be processed. Middleware can modify the request or perform 

actions such as authentication, logging, or request validation.

Middleware can also halt the request and return a response early (e.g., for authentication failures).

5. Request Handling:

The view processes the request. It may:
    Query the database using models.
    Process forms.
    Perform business logic.
    Generate context data for rendering.

6. Template Rendering:

If the view returns an HTML response, Django uses the template engine to render the HTML page. It combines the template with the context data provided by the view.

This involves searching for the template in the specified directories.

7. Response Generation:

After rendering, Django creates an HttpResponse object containing the rendered content (HTML, JSON, etc.) and returns it to the middleware.

8. Middleware Response Processing:

The response then passes through the middleware stack again. Middleware can modify the response before it is sent back to the client (e.g., adding headers, compression).

9. HTTP Response:

Finally, the response is sent back to the client (the user’s browser). The browser then displays the content to the user.


* Summary of Key Components

    - URLs: Route requests to views based on URL patterns.
    - Views: Handle business logic and return responses.
    - Middleware: Process requests and responses globally; can modify or terminate the request/response cycle.
    - Templates: Render HTML responses by combining templates with context data.

* Simplified Version

   → Client Request 
   → Django URLs
   → Middleware (Request Processing) 
   → View Function 
   → Database Models (optional) 
   → Template Rendering (if HTML response) 
   → Middleware (Response Processing) 
   → HTTP Response 
   → Client Response.

