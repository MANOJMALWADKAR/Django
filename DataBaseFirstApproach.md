# Inspecting DataBase And Genrate Models

- first add import any db in pgadmin
- create new project in django 
- then Run this cmd

    python manage.py inspectdb > model.py

- it will create new model.py where all models will create in sec

# Accessing Generated Models Using Django ORM

- view.py

    from django.shortcuts import render

from dbfirstapproachapp.models import Categories


# Create your views here.

def ShowCategories(req):
    categories = Categories.objects.all();

    return render(req,'dbfa/ShowCategories.html',{'Categories':categories})

- urls.py

    path('ShowCategories/',views.ShowCategories)

- ShowCategories.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show Categories</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">
</head>
<body>
    <table class="table">
        <thead>
            <tr>
                <th>Category ID</th>
                <th>Category Name</th>
                <th>Category Description</th>
            </tr>
        </thead>
        <tbody>
            {% for category in Categories %}
                <tr>
                    <td>{{ category.category_id }}</td>
                    <td>{{ category.category_name }}</td>
                    <td>{{ category.description }}</td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</html>