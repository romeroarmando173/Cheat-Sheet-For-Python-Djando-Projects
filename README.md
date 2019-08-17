# Cheat-Sheet-For-Python-Djando-Projects
During coding school we always had to recreate all theses steps for every new project we created. And I just made it faster and easier to create a Django project with these universal set up steps. Hope they help. 


---------------------------------------------------------------------------------------------------------------------


STARTING A DJANGO PROJECT 

MAKE SURE YOU ARE CREATING YOUR PROJECT FROM DJANGO PROGJECTS

1. be in your virutal environment  // after bin, just do source activate 
2. django-admin startproject book_authors_project 
4. cd into your your_project_
5. mkdir apps
6. cd into apps
7. touch __init__.py
9. python ../manage.py startapp your_app_name_here     (you are running this from within apps)
10. cd your way back once or back to your project folder and code . to open visual studio
11. Go to your Project-Level 'settings.py' and write in your app in  'apps.your_app_name_here' ----MAKE SURE YOU TYPE IN YOUR APP CORRECTLY// DO NOT ADD 'URLS' at end of app   
12. Modify the URLS.py at PROJECT flevel, to include the 'my_apps_name' urls file-which we havent created yet. and we also want to make sure to import include     this is step 12 in Patricks cheat sheet


, include


   url(r'^', include('apps.your_app_name_here.urls')),




13. create the urls.py at APP level and add the proper statements to this new urls.py file to set up our routes:


from django.conf.urls import url      # DON NOT ADD AN s AT THE END OF URL
from . import views

urlpatterns = [
    url(r'^$',views.index),       #????????????  # $ dollar sign only done at app level
]



14. Create a def index() in VIEWS.py (AT THE APP LEVEL) to be accessed with the index route: BUT MAKE SURE YOU HAVE AN ACTUAL index.HTML file- which we make in next step 


from django.shortcuts import render, HttpResponse, redirect
from django.contrib import messages
from .models import *
import bcrypt


def index(request):                                     # no values passed via URL
                                                        # context = {                                       
    return render(request, "users_app/index.html")                                                 #     "randomnum": get_random_string(length=14),    
                                                        # }       
                                                        # here you can wrtie: return render(request, "your_app_name/index.html"), context))
                                                        #randomnum is a dummy word #get_random_string was imported


15. TEMPLATE SETUP

  apps
    app_name 
        urls.py
        views.py
        templates(folder)
            app name (folder)
                index.html
        static (folder) make sure it lines up with the templates folder
            app name (folder)
                css (folder)
                    style.css
                js (folder)
                    script.js
                images (folder)
                    image.img




16. ADD THI TO YOUR HTML FILES <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

17. MAKE SURE YOUR HTML HAS THESE:     {% load static %}   
                                        <link rel="stylesheet" href="{% static 'al_br_1/css/style.css' %}">    

 
18. RUN SERVER AND localhost 8000:  python manage.py runserver  YOU CAN ONLY RUN YOUR SERVER FROM THA PROJECT FOLDER LEVEL AND NOT APP LEVEL FOLDER

18. MAKE YOUR TABLES AND DONT FORGET TO MAKE MIGRATIONS AFTER YOU MAKE YOUR TABLES 



COMMON MODELS

class User(models.Model):
    first_name = models.TextField(255)
    last_name = models.TextField(255)
    email = models.TextField(255)
    password = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

class Movie(models.Model):
    creator = models.ForeignKey(Users, related_name=movies) # is ths how this movie model is related to the users model?
    title = models.CharField(max_length=45)
    description = models.TextField()
    release_date = models.DateTimeField()
    duration = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

------------------------------------------------------------------------------------------------------------------------------
class Author(models.Model):
    class Author(models.Model):
    name = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

class Book(models.Model):
    title = models.CharField(max_length=255)
    author = models.ForeignKey(Author, related_name="books")  # here is how this book model is related to the Author model. 
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)


COMMON QUERIES


ClassName.objects.all() - gets all the records in the table
ClassName.objects.all().values()      to see all users in terminal shell

Dave = Author.objects.create(name="Dave Chapelle")
>>> Dave.id      (after you type this command in, you will get his id next in the shell)
>>> Book.objects.create(title="Funny Show", author=Dave)   # this will create book but you must create author first
>>> User.objects.create(first_name="abram",last_name="cacao", email="mando@mando.com", password="123")
19. RUN MIGRATION BUT FIRST MAKE YOUR TABLES

python manage.py makemigrations
python manage.py migrate
                                                                       

20 RUN SHELL python manage.py shell

21. IMPORT MODELS// from apps.your_app_name_here.models import *    // this imports your modules/files into the shell

22. If you get any any errors in creating your table, doubelcheck import and migrations. migrations(updates,) migrate (connects your database)


            HTML HTML HTML HTML HTML HTML HTML HTML HTML HTML HTML HTML HTML HTML


<h1> Your Gold: <span {{request.session.SOMETHING}}</span></h1>

<div id="locations">
            <form action="/find_gold" method="post">
                    {% csrf_token %}
                <h2>Farm</h2>
                <p>(earns 10-20 gold)</p>
                <input type="hidden" name="building" value="Title of book">
                <input type="submit" value="Add this book">       <!-- THIS IS THE BUTTON-->
            </form>

            
</div>





 CSS CSS CSS CSS CSS CSS CSS CSS CSS CSS CSS CSS



MIGRATION/MODEL/DATABASE SET UP

1. ls to make sure you are inside your project level folder 
2. python manage.py makemigrations    // you would use this command after having added something to your database
3. python manage.py migrate
4. run your server: python manage.py runserver YOU CAN ONLY RUN YOUR SERVER FROM THA PROJECT FOLDER LEVEL AND NOT APP LEVEL FOLDER
5. 





EXTRA NOTES

1. when you create a funciton at views.py App Level, you would then NEXT need to create the url function in the urls.py App Level
2. controller file is also known as the views file
3. at project level you always have to go to urls.py and create new url function for every app. 
4. seems that we dont have views.py at pl (project level)
5. http request, you urls.py gets hit first, then your views/controller
6. context is a keyword that we use to send the method into html
7. make sure your database is imported in shell b4 running queries on it
8. nullable type means that it can intake null type/input. so non-nullable values DO NOT intake null values
9. if you make a new method in views for a new html page, then you also have to create a route in your urls.py
10 Make sure you revisit the SQL queries chapter. You’ll have to know how to do JOIN statements as well as how to do SELF joins. Make sure you feel comfortable with complex SQL queries before you take the exam.
11. Make sure you understand how to pass parameters via URL (e.g. http://localhost/users/show/5).
12. Make sure you really understand how to do login and registration. You will need that functionality for the exam.
13. REGEX  regex  user id url(r'^delete_shirt/(?P<shirt_id>\d+)$', views.delete_shirt),



VIEWS.py and URLS.py (APP LVL) NOTES

1. you will have more methods in your views than urls
2. In VIEWS (example): 
        def index(request):
            context = {"authors": Author.objects.all()}		# we're only sending up all the authors
            return render(request, "your_app_name/index.html", context)




