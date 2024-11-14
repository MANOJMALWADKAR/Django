from rest_framework import generics,mixins

class EmployeesList(mixins.ListModelMixin,mixins.CreateModelMixin,generics.GenericAPIView):
    queryset = Employee.objects.all()
    serializer_class = EmployeeSerializer

    def get(self,req):
        return self.list(req)
    
    def post(self,req):
        return self.create(req)

class EmployeesDetails(mixins.RetrieveModelMixin,mixins.UpdateModelMixin,mixins.DestroyModelMixin,generics.GenericAPIView):
    queryset = Employee.objects.all()
    serializer_class = EmployeeSerializer

    def get(self,req,pk):
        return self.retrieve(req,pk)
    
    def put(self,req,pk):
        return self.update(req,pk)
    
    def delete(self,req,pk):
        return self.destroy(req,pk)