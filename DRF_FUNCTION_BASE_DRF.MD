# Setting Up for Development Environment for DRF

* In venv

    pip install djangorestframework 

    pip install markdown  

    pip install django-filter 


- Django Rest Framework (DRF):  

    Purpose: Enables you to build RESTful APIs quickly and efficiently.

    Use: It provides tools for serialization, authentication, and view handling, making it easier to expose your Django models as APIs.

- Markdown:

    Purpose: Adds support for rendering Markdown content in the browsable API.

    Use: This allows you to write documentation or descriptions in Markdown format, making it more readable and visually appealing in the API interface.

- Django Filter:

    Purpose: Adds filtering capabilities to your API views.

    Use: It allows users to filter querysets based on query parameters, making it easier to retrieve specific data. For example, you can filter by fields like date, category, or status directly in the API URL.

* Setup Project

    django-admin startproject drfproviderdemo
    cd drfproviderdemo/
    django-admin startapp drfproviderdemoapp
    code .

- In settings.py 

    INSTALLED_APPS = [
    ...
    'rest_framework',  #add this
    ]

- In urls.py 

    If you're intending to use the browsable API you'll probably also want to add REST framework's login and logout views. Add the following to your root urls.py file.

    urlpatterns = [
    ...
    path('api-auth/', include('rest_framework.urls'))
    ]


# Creating Models And Serializers

* Serialization = model or query sets ---> Dictionaries ---> JSON

* Deserialization = JSON ---> Dictionaries ---> model or query sets

# About Serializers

* NOTE ===> While creating REST_API every Model which is part of REST_API Implementaion should be have SERIALIZER. 

- Serializers are a core part of building APIs with DRF, allowing you to manage data transformations and validations cleanly and efficiently. 

-  They streamline the process of creating APIs and ensure that data integrity is maintained throughout your application.

- You would typically use serializers in your views to handle API requests. 

* Key Features of Serializers

1. Data Conversion:

    - Serializers convert complex data types into a format that can be easily rendered (e.g., JSON).
    - For example, a model instance can be serialized into a JSON object.

2. Validation:

    - Serializers validate incoming data to ensure it meets the required formats and constraints before saving it to the database.
    - You can define custom validation methods for specific fields.

3. Creating and Updating:

    - Serializers can handle creating new instances and updating existing ones by providing methods like create() and update().

4. Field Customization:

    - You can customize which fields are included in the serialized output and how they are represented.

5. Nested Serializers:

    - You can create serializers that reference other serializers, allowing for complex relationships to be represented.


* Create a Employee Model

    class Employee(models.Model):
        FirstName = models.CharField(max_length=30)
        LastName = models.CharField(max_length=30)
        TitleName = models.CharField(max_length=30)
        HasPassport = models.BooleanField()
        Salary = models.IntegerField()
        HireDate = models.DateField()
        Notes = models.CharField(max_length=200)
        Email = models.EmailField(max_length=50,default='')
        PhoneNumber = models.CharField(max_length=20,default='')

* Create Serializer.py


from rest_framework import serializers

from defproviderdemoapp.models import Employee


class EmployeeSerializer(serializers.ModelSerializer):
    class Meta:
        model = Employee
        fields = '__all__'

* Makemigrations and migrate 
* Create the superuser

* In admin.py

    admin.site.register(Employee)


# Implementing All Records

* In views.py 

- Create a employee_list view (here this view is function view where it takes http request and gives http response, 
                                so we will convert this view into API_VIEW)


    @api_view(['GET'])                                               ## here we can add http methods (get,post,put,delete, etc)
    def employee_list(req):
        if req.method == 'GET':
            employees = Employee.objects.all()                      ## returns a queryset containing all employee records.
            serializer = EmployeeSerializer(employees,many=True)    ## convert the queryset into a format (usually JSON)  
            return Response(serializer.data)

* In urls.py 

    path("api/fbvemployees/", views.employee_list)

* Now runserver

# Implementing POST

* Add POST Method in Above View (@api_view(['GET','POST'])) and add elif condition

    elif req.method == 'POST':
        serializer = EmployeeSerializer(data=req.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data,status=status.HTTP_201_CREATED)
        
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)



# Implementing Get By ID

    @api_view(['GET'])
    def employee_details(req,pk):
        try:
            employee = Employee.objects.get(pk=pk)
        except Employee.DoesNotExist:
            return Response(status=status.HTTP_404_NOT_FOUND)
        
        if req.method == 'GET':
            serializer = EmployeeSerializer(employee)
            return Response(serializer.data)

     path("api/fbvemployees/<int:pk>", views.employee_details)


# Implementing Put

- we can add the put functionality in get by id (add 'PUT' method in api_view)

    elif req.method == 'PUT':
        serializer = EmployeeSerializer(employee, data = req.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)

# Implementing Delete

    elif req.method == 'DELETE':
        employee.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)

        