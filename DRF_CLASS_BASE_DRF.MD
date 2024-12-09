class EmployeeList(APIView):
    def get(self,req):
        employees = Employee.objects.all()
        serializer = EmployeeSerializer(employees,many=True)
        return Response(serializer.data)

    def post(self,req):
        serializer = EmployeeSerializer(data=req.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data,status=status.HTTP_201_CREATED)
        
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)
    
class EmployeeDetails(APIView):
    def get_employee(self,pk):
        try:
            return Employee.objects.get(pk=pk)
        except Employee.DoesNotExist:
            raise Http404
        
    def get(self,req,pk):
        employee = self.get_employee(pk)
        serializer = EmployeeSerializer(employee)
        return Response(serializer.data)
    
    def put(self,req,pk):
         employee = self.get_employee(pk)
         serializer = EmployeeSerializer(employee, data = req.data)
         if serializer.is_valid():
                serializer.save()
                return Response(serializer.data)
         return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)
 
    def delete(self,req,pk):
        employee = self.get_employee(pk)
        employee.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)