from rest_framework import filters


    filter_backends = [filters.SearchFilter]
    search_fields = ['FirstName']
    
# SORTING

    #starts with
    search_fields = ['^FirstName']

    #excat match
    search_fields = ['=FirstName']



    #orderingFilter    ( sort with id)
    filter_backends = [filters.OrderingFilter]
    ordering_fields = ['FirstName]
    ordering = ['id']              