# Django coding standard

## Introduction

This document defines the coding standard we shall be using to develop our projects. In the Django tutorial documentation, we have known how to create the folder structure for our projects. Now we shall define how our code should be structured.

In this document, we shall discuss on the following things:
 
 - Coding Style
 - Comment Management
 - Defining Static Values
 - Import Management
 - Database Structure
 - Settings Management
 - Environment Variables
     - Storing environment variables
     - Extracting environment variables
 - Apps Management
 - Models Management
    - Writing Models
    - Issues relating to models and migrations
 - Views Management
    - Writing views
    - Issues relating to views

## Coding Style

 - Unless stated, we will use [PEP8](https://www.python.org/dev/peps/pep-0008/) standard. 
 - Use four spaces for indentation.
 - Use four space hanging indentation rather than vertical alignment as:

        return render(
            request,
            self.template_name,
            {'object': object}
        )
    Instead of:

        return render(request, 
                    self.template_name,
                    {'object': object})
 - Use underscores for function names rather than camelCase.
 - Use InitialCaps for class names.

## Comment Management

In this section, we shall discuss how to write comments in our code. We can use inline comments, function or class level comments or file level comments.

For inline comments, we need to provide two spaces and start writing the comment.
For example,

    input_string = "Hello world."
    formatted_string = input_string.strip(" ")  # remove the whitespace from the string
You should provide two spaces before the `#` sign and a single space after it. Make sure that the comments are short and readable.

Similarly, for functional or class based comments, we will be using `""" """` comment style. Details to be included in comments for functions are:

1. What the function does?
2. What parameters does it take?
3. Ways to call the function.
4. What is returned by the function?

Example:

    def sum(a, b):
        """
        This function adds two numbers provided to it as an argument.
        It expects two integer arguments and returns a integer argument.
        Calling it:
            total = sum(1, 2)
            print(total)
        Make sure that you pass two integer values. 
        In case, any other data types are sent (for example, string),
        the function does not provide the output as expected. 
        """
        return a + b

Details to be included in comments for class are:

1. What is the class defined for?
2. What are the initial arguments it takes?
3. What properties can be overridden?

Example:

    class Person(object):
        """
        This class defines a person with attributes name and age.
        Basically name is a string and age is an integer.
        We can define the name and age of the person object during object creation as
            p = Person("demo", 26)
        """
        def __init__(self, name, age):
            self.name = name
            self.age = age
        
        def concat_fields(self):
            """
            This function returns a string which is formed by 
            concatenating the name and age of a person object.
            To call this function, you can just use p.concat_fields(), 
            where p is a Person object.
            """
            return self.name + ' ' + str(self.age)


## Defining Constants

Contants are required to define some values that will be constant within a function, class, file or the projet as a whole.

We can define constants that can be used within a single class, a single function, a single file or the overall project. Make sure that you can reuse the constant wherever you need. Every constants are written in all caps form. For example:

    DEBUG  = True
Defining constants within function:

    def show_me_what_you_got():
        """
        This function prints a static value.
        """
        WHAT_I_GOT = "power"
        print("I've got the ", WHAT_I_GOT)
For class, we can use the same format as that of functions.

Similarly, for reusing the constant in a single file, we can define it on top of the files after defining the imports.
To use the constant in the whole project, we can define the constant in a file and import it in other files.

Such constants can be of any type. They can be a string, an integer, a list, a dictionary, a tuple, etc.

## Import Management

Order of import:

1. Future imports
2. Standard library
3. Third-party libraries
4. Other Django components
5. Local Django components

We can call these listed orders as import modules.

        #! import_example.py

        # future
        from __future__ import unicode_literals

        # standard libraries
        import json
        import sys
        from itertools import chain

        # third-party
        import bycrypt

        # Django
        from django.conf import settings
        from django.contrib.auth.models import Group
        from django.http.response import (
            Http404, HttpResponse, HttpResponseNotAllowed, 
        )

        # local Django
        from .models import DemoModel

        CONSTANT = "power"

 - Provide a space between different importing modules.
 - Place the imports alphabetically within a single import module.

## Database Structure

In our projects, we will be using normalized database architecture upto 3NF. For user table, we will use the default Django User model. If additional fields are to be added in the User model, we will create a custom user model by inheriting the AbstractUser. In case the fields can be added in user profile, we will create a user profile model using One-To-One relationship between user and user profile.

Creating a custom User model extending the `AbstractUser`:
    from django.contrib.auth.models import AbstractUser


    class CustomUser(AbstractUser):
        """
        Define the fields to be added in Django default User model.
        """
        gender = models.CharField()