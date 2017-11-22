# Django fundamental

Advantage

Python, ORM: Object relation mapping, Admin, Template, Form, Packages
Focus on productivity

Install Django
	Install Python
	Install the pip package manager
	Install virtualevn
	Install Django

	version: Django 1.6 with Python 3.x

Virtualenv allow to create isolated Python environment

For Windows using https://docs.djangoproject.com/en/1.11/howto/windows/

## Create virtual environment using wrapper (better way)

	WinCmd> pip install virtualenvwrapper-win
	Linux> 	Pip install --user virtualenvwrapper
	then
	WindCmd> mkvirtualenv  venv_python3.6
	> workon
	> workon venv_python3.6

If not using wrapper
	Install virtual environment (using wrapper is easier)
		Wincmd> pip install virtualenv
		linux> sudo pip install virtualenv

	Create a new virtual environment 
		> virtualenv venv_python3.6
		With specific python version
		> virtualenv -p path/to/python venv_python3.6
		> cd ~/venv_python3.6/script
		(c:\Users\2036557\venv_python3.6\Lib\site-packages>)
		> activate

## Install Django

	> pip install django
	OR install specific version
	> pip install django==1.6

You will see django after install here
	> dir c:\Users\2036557\venv_python3.6\Lib\site-packages

Do some test
	> cd c:\Users\2036557\venv_python3.6\Lib\site-packages
	> python
	>>> import django
	>>> django.VERSION
	>>> quit()

## Creating a new project

	>django-admin.py startproject boardgames

## Start project
	> cd boardgames
	> python manage.py runserver

## Django Apps
- An app is a Python package
with it's own models, views, templates, url mappings
- Keep your apps small and simple. Each app should have only one purpose
- App can be reusable between projects
- To create app

	> python manage.py startapp main
- Add new page to view then add main app to boardgames/setting.py
- Add new urls to urls.py using regular expression. ^ means start, $ means end. without ^ or $ will be open start or open end string.
More about python regex: http://goo.gl/5uJsfy

## Django Views
	def home(request):
		return HttpResponse("Hello, World!")
	
Move generation of HTML to a template instead
## Templates
- Can render HTML or any kind of text-based format
- To render a template from a view:
	use django.shortcuts.render
- Templates go in the templates/dir of your app
	project/app/templates/app/template.html
	boardgames/main/templates/main/home.html

## Static Files
- For non-dynamic content like CSS, JavaScript, images
- May be hosted seperately
- In setting.py
	STATICFILES_DIRS = (os.path.join(BASE_DIR, "static"),)
- In templates:
	{% load staticfiles %} at start template
	{% static 'path/to/file' %} to refer to static content
	e.g:
	<link rel="stylesheet"
		href="{% static 'bootstrap/css/bootstrap.min.css' %}">

## Model Template View

Like MVC, but Template like View, View as Controller, and Model

create new app ticktactoe and add the app to setting.py
In tictactoe/models.py add models class then run
	> python manage.py migrate

Each model class maps to a database table
and it is subclasses of django.db.models.Model class

Each attribute of the model represents a database field
reference http://goo.gl/rgqWZu

To reate admin user/password
	> python manage.py createsuperuser
change password
	> manage.py changepassword <user_name>

e.g.: admin/adminpassword

To install sqlite3
	> sudo apt-get install sqlite3
for windows : download sqlite-tools-win32-x86-3120200.zip from 
https://www.sqlite.org/download.html

Start a shell for database (need sqlite3)
	> python manage.py dbshell
	sqlite> drop table tictactoe_game;
	sqlite> .exit
unapply all migration on tictactoe
	> ython manage.py migrate --fake tictactoe zero

## Admin
An auto-generated user interface to edit your data
	Need to register your models in your apps' admin.py
	admin.site.register(MyModel)

Very customizable
	For documentation, see: http://goo.gl/70YyPC

Implement __str__ for your model classes
