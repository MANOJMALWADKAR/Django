# What is Django REST Framework (DRF)?

- Django REST Framework (DRF) is a open-source, powerful and flexible toolkit for building Web APIs in Django.

* Key Features

1. Serialization:
   DRF provides an easy way to convert complex data types, such as Django models or querysets, into Python data types (usually dictionaries), which can then be easily converted into JSON or XML. It also supports deserialization, where incoming data (usually JSON) is converted back into Django model instances or Python objects.

2. Authentication and Permissions:
   DRF includes built-in support for a variety of authentication schemes (e.g., Token authentication, Session-based authentication, OAuth). It also allows the implementation of custom permission classes to restrict access to API views based on user roles, actions, or other criteria.

3. ViewSets and Routers:
   DRF simplifies the process of defining views for your APIs by providing viewsets. Viewsets automatically handle common actions (such as list, create, retrieve, update, and destroy) for API resources. Routers automatically generate URL configurations for your viewsets, reducing boilerplate code.

4. Pagination:
   DRF offers built-in support for pagination, allowing developers to manage large datasets and return results in chunks, improving performance.

5. Throttling and Rate Limiting:
   DRF includes tools for rate-limiting API requests, preventing abuse by limiting how many requests a client can make in a given period.

# Why should you use DRF?

1. Seamless Django Integration: DRF works effortlessly with Django’s ORM, authentication, and views, making it easy for Django developers to build APIs.

2. Rapid API Development: DRF reduces boilerplate code with tools like serializers, viewsets, and routers, speeding up the development of RESTful APIs.

3. Authentication and Permissions: Built-in support for various authentication methods (e.g., token, session) and customizable permission classes ensures secure and role-based access.

4. Browsable API: DRF provides a user-friendly web interface for testing and interacting with the API during development.

5. Advanced Features: DRF supports pagination, filtering, searching, rate limiting, and hyperlinked APIs, making it flexible for complex API needs.

6. Extensive Documentation and Community: DRF has clear documentation and strong community support, ensuring quick learning and troubleshooting.

# How To Create

1.  Create project
    django-admin startproject product_api
    cd product_api
    python manage.py startapp products

2.  Set up Django REST framework(in INSTALLED_APPS)
    'rest_framework', # Add DRF
    'products', # Add your app here

3.  Define Product Model

    class Product(models.Model):
    name=models.CharField(max_length=100)
    description=models.TextField()
    price=models.DecimalField(max_digits=10,decimal_places=2)

    def **str**(self):
    return self.name

4.  Create and Apply Migrations

    python manage.py makemigrations
    python manage.py migrate

5.  Create a Serializer for the product

    from rest_framework import serializers
    from .models import Product
    class ProductSerializer(serializers.ModelSerializer):
    class Meta:
    model = Product
    fields = ['id', 'name', 'description', 'price']

6.  Create a View for API
