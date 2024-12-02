2. Class Based View

# views.py

from rest_framework import generics
from .models import Book
from .serializers import BookSerializer

# Create

class BookCreateView(generics.CreateAPIView):
queryset = Book.objects.all()
serializer_class = BookSerializer

# Read

class BookListView(generics.ListAPIView):
queryset = Book.objects.all()
serializer_class = BookSerializer

class BookDetailView(generics.RetrieveAPIView):
queryset = Book.objects.all()
serializer_class = BookSerializer

# Update

class BookUpdateView(generics.UpdateAPIView):
queryset = Book.objects.all()
serializer_class = BookSerializer

# Delete

class BookDeleteView(generics.DestroyAPIView):
queryset = Book.objects.all()
serializer_class = BookSerializer

# urls.py

from django.urls import path
from . import views

urlpatterns = [
path('books/', views.BookListView.as_view()),
path('books/<int:pk>/', views.BookDetailView.as_view()),
path('books/create/', views.BookCreateView.as_view()),
path('books/<int:pk>/update/', views.BookUpdateView.as_view()),
path('books/<int:pk>/delete/', views.BookDeleteView.as_view()),
]
