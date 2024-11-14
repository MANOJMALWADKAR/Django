
from rest_framework import viewsets

class EmployeeViewSet(viewsets.ModelViewSet):
    queryset = Employee.objects.all()
    serializer_class = EmployeeSerializer


    urls.py

    from rest_framework.routers import DefaultRouter

    router = DefaultRouter()
    router.register('api/EmployeeViewSet',views.EmployeeViewSet)

    urlpatterns = [
        path('',include(router.urls)),
    ]
