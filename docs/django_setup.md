# Introduction to Django

## What is the Django framework?

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

It is maintained by the Django Software Foundation(DSF). The core goal of Django is to make complex, database-driven websites easy to create. 

## How is Django different from other coding frameworks?

**Easy to learn**

The learning curve of Python/Django suggests that it is easy to learn. This makes it easier for new developers to grasp the Django architecture and coding format in less time.

**Build high-load projects**

Django helps us to build huge projects with multiple functionalities. Some projects built on django are Youtube, Pinterest, Instagram, etc.

**Fast**

Django helps in making it both cost-effective and efficient products. Thus it becomes an ideal solution for developers having a primary focus on deadlines.

**Secure**

Some of the common mistakes include SQL injection, cross-site request forgery, clickjacking, and cross-site scripting. To effectively manage usernames and passwords, the user authentication system is the key. It is ensured that developers don’t commit any mistakes related to security.
In-built user authentication, user permission management and object-level permissions of Django makes sure that security of the system is maintained effectively.

**Exceedingly scalable**

Some of the busiest sites on the Web leverage Django’s ability to quickly and flexibly scale.

## Systems built in Django

 - Instagram
 - Mozilla
 - Youtube
 - Pinterest
 - Disqus
 - Open stack
 - Spotify
 - Bitbucket
 - Dropbox, etc.

## What are the scopes of Python/Django?

1. Python is one of the most used languages in 2016, with major tech giants including Google and Quora being its users.
2. It also has a huge open-source fanbase, currently ranking 5th in the github repository trends. Also, according to Google Trends, economically developed countries - US, China and South Korea - are its top-3 users, which further strengthens its position.
3. Django is the most popular and extensive among all of the python frameworks. It is good for developing complex applications with many individual parts. Its major users include Pinterest, Instagram, Mozilla, The Washington Times, Disqus, Bitbucket and Nextdoor.
4. The popularity of the framework is also on a constant rise.
5. Python being a popular language in ML and Data analysis, users prefer Django to build the web-application to integrate the results and functionalities written in Python.

## Introduction to Django architecture

Django uses MVC(Model-View-Controller) architecture similar to other web application frameworks. But the architecture terminologies are different from other frameworks. 

**Model**

Model is used to define the database tables structure for the system.

**View**

View is used to configure the templates for UI. In Django, views are handled as templates. Views are not the regular views we see in other MVC frameworks but serve as controllers in Django.

**Controller**

Controller is used to handle requests and responses of the system. Django views serve as controllers for Django.

Hence, we can say that Django is a MVT(Model-View-Template) architecture framework. Don’t confuse Django view as that of other MVC framework.

Now, let’s go through each component that is required to create a normal web application in Django.

### Model

Model is used to define how the database tables should be. It defines the tables, their attributes, relations, etc. Models are stored in a **“models.py”** file inside the project or app. We will discuss projects and apps later on this document.

    #!models.py
    from django.db import models
        
        
    class DemoTable(models.Model):
        name = models.CharField(max_length=255)
        phone = models.CharField(max_length=255)
        age = models.IntegerField()
        date = models.DateTimeField()

**Don’t worry about the code written above if you don’t get it. We will discuss these later.**

### URL

Urls are routes that redirects the user request to a django view. Urls are basically written in regular expression format and (after django2) normal string format. Urls are included in the **urls.py** file.

### View

Views act as controllers for django. Any request from the user-end is redirected to the view from a url. After the request is received by the view, it processes the request and sends the required data to the user-end in different formats like HttpResponse, JsonResponse, Redirects, etc.. 

### Template

Templates are the UI used for the user end. Many projects may not involve the use of any templates(if any front-end framework is used). But, templates are in a basic way the UI components like HTML files that show the data returned from django views.

## Django Project Setup

Let’s begin by setting up our first Django project. For this, we need to make sure that we create a new virtual environment for each project we will be creating in the future. 

### What is a virtual environment?

Virtual environment helps to keep dependencies required by each project separated by creating different python virtual environments for them. It is required that dependencies of a project do not affect other projects.

### Installing virtual environment

To install a virtual environment, first we need to make sure that our computer has python installed in it. Python3 is preferred as Python2 has been depreciated from 2020. Also, install pip for the suitable python version.

After everything is installed, you can use the following command to install virtualenv:

    pip install virtualenv
    pip3 install virtualenv (for python3)

Now you can create a virtual environment by the following command:

    virtualenv <location_of_virtual_env> -p <python_version>

For example:

    **In Linux**
    virtualenv ~/.virtualenvs/venv -p python3
    **In Windows**
    virtualenv C:\Users\public\virtualenvs\venv -p C:\Python\Python36\python.exe
Now activate the virtual environment you have just created as:

    **In Linux**
    source ~/.virtualenvs/venv/bin/activate
    **In Windows**
    C:\Users\publc\virtualenvs\venv\Scripts\activate
**Make sure you get the path correct to the virtual environment.**

You can know if the virtual environment is activated by checking if (venv) is seen in the beginning of the command in your terminal or command line interface. For example:

    (venv) C:\Users\public\Desktop> 
Now you are ready to install required packages inside the virtual environment.
To deactivate the virtual environment you can use the following command:

    (venv) C:\Users\public\Desktop> deactivate
    C:\Users\public\Desktop>

### Installing packages inside virtual environment

To install packages inside the virtual environment, make sure that the virtual environment is activated first. Then you can install any packages using pip. For example, you can install Django with following command:

    pip install django
There are different ways to install a package. You can install a package with specified version as:

    pip install django==2.0.10

Similarly, you can install the package of latest version as:

    pip install -U django
Also, you can just specify the package name and the available version is directly installed by the system:
    pip install django

## Installing Requirements

You can install django by using any of the methods provided above. But it is recommended you use -U because it helps you to get the latest versions. But sometimes when the project is already existing, you need to find the exact version used in that project and install django of the same version. Normally, the required packages can be found in requirements.txt file of an existing project. In case that you encounter a requirements.txt file, you can install all the packages listed in the file by using the following command:

    pip install -r requirements.txt
This command will make sure all the packages required for the project will be installed with the exact version listed in the file.

## Start Project

After you have activated your environment and installed Django in it, you will be able to start a new project. There are two ways in which we can set up your project.

**Note: We will be using the second approach for our projects.**

In the first approach, go to your folder where you want to keep your Django projects. I will be creating a new directory named django-projects in my home directory.

    mkdir django-projects

Then inside django-projects, we will create a django project named “**demo**”.

    django-admin startproject demo
Now we can see a “demo” folder created inside django-projects. Let’s look at the folder structure for this project.

    django-projects/
        demo/
            demo/
                __init__.py
                settings.py
                urls.py
                wsgi.py
            manage.py
Our demo project consists of a file named manage.py and a folder named demo. manage.py is automatically created for each project. The use of manage.py file is the same as that of django-admin but we can specify django environment variables which will be used by settings.py in our project. Similarly, inside the demo app of the demo project, we can see various files like `__init__.py`, `settings.py`, `urls.py` and `wsgi.py`. These files are also automatically created and are useful to run our project. settings.py file helps us to define different variables for our project environment like `SECRET_KEY`, `ALLOWED_HOSTS`, `MIDDLEWARE`, `TEMPLATES`, etc. Also, it helps to manage how static files and media files are served. The main file that is required for project setup is settings.py file.

In Django 3 version, `wsgi.py` is replaced by `asgi.py` file. We will discuss this part if required. `wsgi.py` is used to run our project in a server environment.

`urls.py` file is used to define the url routes that will be included in our project. We will include urls from other apps in this file.

Now we will define other apps we will require sitting in the __“demo”__ app folder. But be aware that __“demo”__ is both the project folder and an app folder. The folder in the upper hierarchy is the project folder and the folder with the same name inside the project folder is an app folder. This has caused some misunderstanding. To solve this misunderstanding and having a good folder structure is what we are trying to achieve. 

Second approach helps us to solve the folder name redundancy and misunderstanding. In this approach, go to your folder where you will store your django projects. I will use the django-projects folder. Follow the below steps to get a good folder structure:

First, create a folder inside your django projects folder(django-projects) in my case with any name. For example: django-blog. 

    mkdir django-blog
Then, go inside the django-blog project and create a project inside django-blog.
    django-admin startproject blog .
This creates only a manage.py file and blog folder inside our django-blog folder. Unlike the previous approach, we have removed the redundancy of folder names within a project. Now our new folder structure will be:

    django-blog/
        blog/
            __init__.py
            settings.py
            urls.py
            wsgi.py
        manage.py
As you can see from the image above, we have a django-blog folder containing a blog folder and manage.py file.

For each app to be created in this project, we will create them inside the blog app. For this, we will go inside the blog folder:

    cd blog
Create a new app labelled core:

    django-admin startapp core
In settings.py file, register the app as:

    # Application definition
 
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]
    
    INNER_APPS = [
        'blog.core',
    ]
    
    INSTALLED_APPS += INNER_APPS
For other apps, we will use the same method to create and register the app.

**Note: Please use the second approach for development.**

## Folder Structure

After setting up the project following the second method as above, we will have a folder structure as shown below:

    django-blog/
        blog/
            core/
                migrations/
                __init__.py
                admin.py
                apps.py
                models.py
                tests.py
                views.py
            __init__.py
            settings.py
            urls.py
            wsgi.py
        manage.py

## URLS management

The urls.py file in the main folder, i.e. blog folder is the main __urls__ file. Django checks this file to find the routes requested by the user. So, urls of other apps will be included in this file. Let’s create a `urls.py` file for our core app(`urls.py` files are not created automatically for the apps as that of the main app).

    from django.urls import include, path
    
    from blog.core import views
    
    urlpatterns = [
        path('', views.homepage, name="home"),
    ]
Here I have created a route that calls the homepage view. __homepage__ view is called by importing the views file of `blog.core`. To import anything in this folder structure, we need to make sure that we first provide the main app name (e.g. blog) followed by the sub-app name (e.g. core).

    from <main_app_name>.<sub_app_name>.<file_name> import *
 
    OR
    
    from <main_app_name>.<sub_app_name> import <file_name>
From the first method, we can directly use the class, function or object name directly. Whereas, using the second method we need to use the class, function, object, or variable name using __“<file_name>.<required_componen>”__. For example, the way I imported homepage in the urls.py file of the core app.

Now define a view named homepage inside __core app’s views.py__ file

    from django.shortcuts import render
    from django.http import HttpResponse
    
    
    def homepage(request):
        return HttpResponse("Hello world!!!")
Now we need to include this route in our main ‘urls.py’ file as

    #! blog/urls.py

    """
    blog URL Configuration

    The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/2.2/topics/http/urls/
    Examples:
    Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
    Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
    Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
    """
    from django.contrib import admin
    from django.urls import path, include # import include
    
    urlpatterns = [
        path('admin/', admin.site.urls),
        
        path('', include('blog.core.urls')),
    ]
Now start the server

    python manage.py runserver
Before starting the server, make sure you have activated the virtual environment for this project. After starting the server, you will see the following output in your console

    Watching for file changes with StatReloader
    Performing system checks...

    System check identified no issues (0 silenced).

    You have 17 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.

    August 13, 2020 - 11:13:40
    Django version 2.2.6, using settings 'blog.settings'
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.
To remove the error of migration as shown above, you need to perform migrations. For this you need to configure your database settings in settings.py file (Or leave it as is to use sqlite database). Run the following command to run migrations:

    python manage.py migrate
After this, the console output won’t show any error. Now our application will run on localhost:8000 or 127.0.0.1:8000

If you want to change the port where our application runs you need to start the server using:

    python manage.py runserver <port>
If you want any other person in your internal network (like office network, home network) to view your application or access any API from this application from their personal computer, you need to run the server using:

    python manage.py runserver 0.0.0.0:<port>
Then the next person can access your application by entering the following in their browser:

    http://<your_ip_address>:<port>
__Note: Make sure you and the other person are connected to the same network.__

Now let’s view the output in the browser. Go to your browser and enter localhost:8000 or 127.0.0.1:8000 in your browser url. Then you will see "Hello world!!!" displayed in the screen. __Success!!!__

Let’s go through how this output is obtained.

1. When you enter localhost:8000 in your browser, our application searches for an empty route, i.e. path(‘’). It is because we have not entered anything after localhost:8000. 
2. The application first searches through routes listed in urls.py file in a top-to-bottom manner.
3. Then it finds the path 	`path(‘’, include(‘blog.core.urls’)),`
4. Then it knows that it needs to search for routes inside our core app. So, in the next step, it searches the url route in core’s urls.py file.
5. Then it finds the path that meets it’s requirement, i.e. `path(‘’, views.homepage, name=”home”),`
6. If the application does not find any suitable route, 404 error is sent.
7. After it has found the suitable route, it calls the respective view, i.e. homepage.
8. The system then executes the function homepage and returns a text to the browser “Hello world!!!”. It is because we have returned a HttpResponse from the homepage view. A view can return a HttpResponse, HttpResponseRedirect, Response, JsonResponse, render a template, etc.

We have now created a project in Django. Follow the above suggestions to format the project folder structure. For coding standards, we will use PEP8 standards strictly.

I will provide other documents relating code formatting we will be using to develop our projects.


