1. Function-Based Views (FBVs)

# models.py

from django.db import models

class Book(models.Model):
title = models.CharField(max_length=255)
author = models.CharField(max_length=255)
published_date = models.DateField()

    def __str__(self):
        return self.title

# serializers.py

from rest_framework import serializers
from .models import Book

class BookSerializer(serializers.ModelSerializer):
class Meta:
model = Book
fields = '**all**'

# views.py

from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status
from .models import Book
from .serializers import BookSerializer

# Create a book

@api_view(['POST'])
def create_book(request):
if request.method == 'POST':
serializer = BookSerializer(data=request.data)
if serializer.is_valid():
serializer.save()
return Response(serializer.data, status=status.HTTP_201_CREATED)
return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

# List all books

@api_view(['GET'])
def list_books(request):
if request.method == 'GET':
books = Book.objects.all()
serializer = BookSerializer(books, many=True)
return Response(serializer.data)

# Retrieve a single book

@api_view(['GET'])
def get_book(request, pk):
try:
book = Book.objects.get(pk=pk)
except Book.DoesNotExist:
return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method == 'GET':
        serializer = BookSerializer(book)
        return Response(serializer.data)

# Update a book

@api_view(['PUT'])
def update_book(request, pk):
try:
book = Book.objects.get(pk=pk)
except Book.DoesNotExist:
return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method == 'PUT':
        serializer = BookSerializer(book, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

# Delete a book

@api_view(['DELETE'])
def delete_book(request, pk):
try:
book = Book.objects.get(pk=pk)
except Book.DoesNotExist:
return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method == 'DELETE':
        book.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)

# urls.py

from django.urls import path
from . import views

urlpatterns = [
path('books/', views.list_books),
path('books/<int:pk>/', views.get_book),
path('books/create/', views.create_book),
path('books/<int:pk>/update/', views.update_book),
path('books/<int:pk>/delete/', views.delete_book),
]
