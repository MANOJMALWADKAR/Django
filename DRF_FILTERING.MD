pip install django_filters

# setting.py (GLOBAL LEVEL APPROACH)

installed_app = [

'django_filters',

]

REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS':['django_filters.rest_framework.DjangoFilterBackend']
}

views.py

        filterset_fields = ['FirstName']


# OR (CLASS LEVEL APPROACH)

views.py

    from django_filters.rest_framework. import DjangoFilterBackend

    filter_backends = [DjangoFilterBackend]

    filterset_fields = ['FirstName']



