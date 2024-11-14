# settigs.py (GLOBAL LEVEL WAY)

* note ==> this type paginatio nworks with generic and viewsets

REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 2
}


# CLASS LEVEL WAY

    
    from rest_framework.pagination import PageNumberPagination

    class EmployeeCustomPagination(PageNumberPagination):
    page_size = 1  

    class EmployeeViewSet(viewsets.ModelViewSet):
        queryset = Employee.objects.all()
        serializer_class = EmployeeSerializer
        pagination_class = EmployeeCustomPagination


