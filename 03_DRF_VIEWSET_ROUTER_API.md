3. ViewSets and Routers (The DRF Way)
   ViewSets are one of the most powerful features of DRF and allow you to handle all CRUD operations with minimal code. DRF provides automatic handling for create, read, update, and delete.

# views.py

from rest_framework import viewsets
from .models import Book
from .serializers import BookSerializer

class BookViewSet(viewsets.ModelViewSet):
queryset = Book.objects.all()
serializer_class = BookSerializer

# urls.py

from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import BookViewSet

router = DefaultRouter()
router.register(r'books', BookViewSet)

urlpatterns = [
path('', include(router.urls)),
]
