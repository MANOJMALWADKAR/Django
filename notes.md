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
