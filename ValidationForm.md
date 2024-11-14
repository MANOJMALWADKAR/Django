# Starting New Project Related To Form Validation

- django-admin startproject validationproject
- cd validationproject
- django-admin startapp validationdemoapp

- after creating project open it in vscode
- create new folder called templates
- configure setting for templates folder
- in settings.py add variable
    TEMPLATES_DIR = BASE_DIR / 'templates'
- add this TEMPLATES_DIR variable in 
    TEMPLATES[
        {
        'DIRS' : [TEMPLATES_DIR]
        }
    ]
    
# Create New Model In Models.py 

from django.db import models

# Create your models here.

from django.db import models

class UserRegistration(models.Model):
    username = models.CharField(max_length=15,verbose_name="user Name")

    username = models.CharField(
        max_length=15,verbose_name="user Name",
        validators=[MinLengthValidator(5)]
        )

    password = models.CharField(max_length=15,verbose_name="Password")

    password = models.CharField(
        max_length=15,verbose_name="Password",
        validators=[MinLengthValidator(6)],
        )

    confirm_password = models.CharField(max_length=15,verbose_name='Confirm Password')

    confirm_password = models.CharField(
        max_length=15,verbose_name='Confirm Password',
        validators=[MinLengthValidator(6)],
        )

    gender = models.CharField(max_length=10,verbose_name='Gender')
    country = models.CharField(max_length=20,verbose_name='Country') 
    date_of_birth = models.DateField(verbose_name="Date Of Birth")

    email = models.EmailField(verbose_name='Email')
    postal_code = models.IntegerField(verbose_name='postal code')

    postal_code = models.IntegerField(
        verbose_name='postal code',
        validators=[MinValueValidator(1000),
                    MaxValueValidator(9999999)],
        )

    phone_number = models.IntegerField(max_length=15, verbose_name='phone number')   

    profile = models.TextField(verbose_name='Profile', blank=True)
    website_url = models.URLField(verbose_name='Website URL')
    terms_conditions = models.BooleanField(verbose_name='Terms & Condition')
    favwebsite_url = models.CharField(max_length=256)
    
# Create forms.py

- import forms from django

    from django import forms

- also import UserRegistration from models
    
    from validationdemoapp.models import UserRegistration

-  user registration functionality for validation

    class UserRegistrationForm(forms.ModelForm):

        class Meta:
            model = UserRegistsration
            fields = '__all__

            genders = [
                  {"male","Male" },
                  {"female","Female"}
            ]

            country = [
                  ("select", "Choose Country"),
                  ('India','India')
            ]

            widgets = {
                  'password': PasswordInput(),
                  'confirm_password': PasswordInput(),
                  'gender': RadioSelect(choices=genders),
                  'country': Select(choices=country),
                  'date_of_birth': DateInput(attrs={'type':'date'}),
                  'email': EmailInput(),
                  'website_url': URLInput()
            }

# Connect The validationdemoapp to validationdemoproject

- in urls.py(validationdemoproject)

    from validationdemoapp import views
    path('signup/',views.SignUp,name='signup'),

# Create SignUp view in views.py

    from django.shortcuts import render

    from validationdemoapp.forms import UserRegistrationForm

    def SignUp(req):

    if req.method == 'POST':
        form = UserRegistrationForm(req.POST)

        if form.is_valid():
            #form.save()
            return render(
                    req,
                    'validationdemoapp/Home.html' 
                )
    else:
            form = UserRegistrationForm()
            
    return render(req,
                    'validationdemoapp/SignUp.html',
                    {'form':form})

# Create SignUp.html

     <div class="container mt-5">
        <center><h2>User Form</h2></center>
        <br>
        <form method="post">
            {% csrf_token %}
            <table class="table">
                <h1>hi</h1>
                {{form.as_table}}
            </table>
            <button type="submit" formnovalidate="formnovalidate" class="btn btn-primary">Submit</button>     # formnovalidate is html attr. which stop                                                                                                     validation from html side
        </form>
    </div>

# Add To DB

- python manage.py makemigrations
- python manage.py migrate
- python manage.py runserver


# Implementing Clean Method for Individual Field (Field Level Validation)

- We can use this type validation on particular single field 
eg.
    def clean_phone_number(self):
            iphonenumber = self.cleaned_data.get('phone_number')
            if iphonenumber:
                    pattern = re.compile(r"(0|91)?[6-9][0-9]{9}")
                    if not re.fullmatch(pattern,iphonenumber):
                        raise forms.ValidationError('Inavalid Phone Number')
                    return iphonenumber


# Implementing a Single Clean Method for entire Form (Form Level Validation)

- Here in this Validation we can add validaition on every field in single clean function
eg. 
    def clean(self):
            cleaned_data = super().clean()
            ipassword = cleaned_data.get('password')
            iconfirm_password = cleaned_data.get('confirm_password')

            if ipassword and iconfirm_password:
                  if ipassword != iconfirm_password:
                        raise forms.ValidationError('Passwords do not match')
            

            iusername = cleaned_data.get('username')
            ipassword = cleaned_data.get('password')

            if ipassword and iusername:
                  if ipassword == iusername:
                        raise forms.ValidationError('username can not be same as password')
                  
            country = cleaned_data.get('country')
            if country == 'select':
                  raise forms.ValidationError('Please Choose country from list ')
            
            terms_condition = cleaned_data.get('terms_conditions')
            if not terms_condition:
                  raise forms.ValidationError('Please agtee to terms and condition')

            return cleaned_data


# Rendering Custom Errors Messages

- We will render custom error messages if the built-in validation fails. 

eg. message attri. in the validator

    username = models.CharField(
        max_length=15,verbose_name="user Name",
        validators=[MinLengthValidator(5,message='Please enter unique username more than 5 letters')]
        )


# Styling error messages

- If we hover the error messages on browser and then go to inspect, then it shows the class of that error messages

- By getting that class we can apply our custom css to it

eg.     
    .errorlist{
        color:'red'
    }






