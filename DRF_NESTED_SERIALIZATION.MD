# Create Two MOdels along Employee

class Department(models.Model):
    DeptName = models.CharField(max_length=30)
    LocationName = models.CharField(max_length=30)

    def __str__(self):
        return self.DeptName
    
class Country(models.Model):
    CountryName = models.CharField(max_length=30)

    def __str__(self):
        return self.CountryName

* In Employee Model add this newly created models

    Department = models.ForeignKey('Department',default=0,on_delete=models.CASCADE,related_name="Departments")
    Country = models.ForeignKey('Country',default=0,on_delete=models.CASCADE,related_name="Countries")


# Create Serializers for Department and COuntry

    class DepartmentSerializer(serializers.ModelSerializer):
    employees = EmployeeSerializer(read_only=True,many=True,source='Departments')
    class Meta:
        model = Department
        fields = '__all__'

    class CountrySerializer(serializers.ModelSerializer):
        employees = EmployeeSerializer(read_only=True,many=True,source='Countries')
        class Meta:
            model = Country
            fields = '__all__'


# Create views of both 

      
    class DepartmentViewSet(viewsets.ModelViewSet):
        queryset = Department.objects.all()
        serializer_class = DepartmentSerializer

    class CountryViewSet(viewsets.ModelViewSet):
        queryset = Country.objects.all()
        serializer_class = CountrySerializer

# Add Path of both in urls.py

    router.register('api/DepartmentViewSet',views.DepartmentViewSet),
    router.register('api/CountryiewSet',views.CountryViewSet),

# Make Migrations and migrate cmd

# Runserver