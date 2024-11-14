# Configuring CORS

* Add this follwing in the project where you want to send data 

- pip install django-cors-headers

installed_app = [
      'corsheaders',
]

middleware = [
    'corsheaders.middleware.CorsMiddleware',
]

- CORS_ORIGIN_ALLOW_ALL = True  # anyone who has server web api can access resource (global like)

CORS_ALLOWED_ORIGINS = [
    'http://localhost:9000',    # Allowed to only this server (data shared with this server)
]


# Create New Project To Fetch data from above project

- views.py 

    API_BASE_URL = 'http://127.0.0.1:8000/api/EmployeeViewSet/'

    def getallemployees(req):
        #fetch the list of employees from the DRF API
        response = requests.get(f'{API_BASE_URL}')
        # print(response)

        if response.status_code == 200:
            try:
                employees = response.json() 
            except ValueError:
                employees = []
        else:
            employees = []

        return render(req,'drfconsumerapp/EmployeesList.html',{'employees':employees})

- html 

                {% for employee in employees %}
                    <tr>
                        <td>{{ employee.id }}</td>
                        <td>{{ employee.FirstName }}</td>
                        <td>{{ employee.LastName }}</td>
                        <td>{{ employee.TitleName }}</td>
                        <td>{{ employee.Salary }}</td>
                    </tr>
                {% endfor %}

- urls.py

    path('employees/getall',views.getallemployees,name='getallemployees')