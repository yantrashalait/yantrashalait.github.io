# Django Rest Framework(DRF)

## Introduction

DRF is a django-package that helps us to build RESTFul APIs for our system. APIs are
used to transfer data from one platform to another. Although there are some other 
packages in Django that help us to build RESTFul APIs, we will be using DRF. 

Commonly, to create a API using DRF, we only need three files:

##### Urls
This file is used to define the routes of the API endpoints. It is same as that 
of a normal urls.py file in django. We can also define routers in urls.py file. 

While using a ModelViewSet, we don't need to define a separate url path for each 
of the operation, but we can create routers for such ViewSets and the url paths
are automatically generated for the given ViewSet. We will discuss about this later.
##### Serializers
Serializers are used to convert the queryset and model objects into python data-types
which can be easily rendered into JSON or XML contents. Similarly, serializers
also allow us to convert the parsed data from the incoming data into complex types.

Serializers act like a Django Form. It helps us to define the data fields, types of
data fields, etc. to be sent as a response. 
##### Viewsets
Viewsets are like views in Django. It is called when a request is made to a specific
url path. Then it collects the data, performs operation on the collected data and sends
out the required data as response.

It uses a serializer to send out the data in correct format(i.e. either JSON or XML).
Also, the serializer helps the viewset to restrict the data fields to be sent out as
a response.




