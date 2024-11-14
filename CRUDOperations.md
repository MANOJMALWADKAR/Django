# Performing Bulk Insert Operation Using ModelFormFactory

# Create Model and Apply Migrations

- In models.py 

    class PartTimeEmployee(models.Model):
        FirstName = models.CharField(max_length=30)
        LastName = models.CharField(max_length=30)
        TitleName = models.CharField(max_length=30)

- python manage.py makemigrations
- python manage.py migratess

# Creating Dynamic Form Using MOdelFormFactory

* Purpose: The DynamicPartTimeEmployeeForm allows for more flexibility by removing the requirement that users must fill out every field when submitting the form.

- Creating the PartTimeEmployeeForm:

    PartTimeEmployeeForm = modelform_factory(PartTimeEmployee, fields=['FirstName', 'LastName', 'Title'])

    - This line uses modelform_factory to dynamically create a form class for the PartTimeEmployee model.
    - It includes only the specified fields: FirstName, LastName, and Title.
    - This form can now be used to create or update instances of PartTimeEmployee.

- Defining DynamicPartTimeEmployeeForm:

    class DynamicPartTimeEmployeeForm(PartTimeEmployeeForm):
    def __init__(self, *args, **kwargs):
        super(DynamicPartTimeEmployeeForm, self).__init__(*args, **kwargs)
        for field in self.fields.values():
            field.widget.attrs.pop('required', None)

    - The __init__ method is overridden to customize the form during its initialization.
    - super().__init__(*args, **kwargs) calls the parent class’s constructor, ensuring that the form is set up with the initial data and any other parameters.
    
    - The loop for field in self.fields.values(): iterates through all the fields in the form.
    - field.widget.attrs.pop('required', None) removes the required attribute from each field’s widget, making all fields optional instead of mandatory.

# Create View And Template For Bulk Insertion