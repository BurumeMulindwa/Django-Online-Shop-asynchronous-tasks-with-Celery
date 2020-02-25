# Django-Online-Shop-asynchronous-tasks-with-Celery
This is a project to integrate Celery into a Django Project and create Periodic Tasks.


Asynchronous Tasks With Django and Celery
This is a project to integrate Celery into a Django Project and create Periodic Tasks.
This project utilizes Python 3.4, Django 1.8.2, Celery 3.1.18, and Redis 3.0.2.

 “Celery is an asynchronous task queue/job queue based on distributed message passing. It is focused on real-time operation, but supports scheduling as well.” 
Setup
Make sure to activate a virtualenv, install the requirements. Then fire up the server and navigate to http://localhost:8000/ in your browser. You should see the familiar “Congratulations on your first Django-powered page” text. When done, kill the server.
Next, install Celery using pip:
$ pip install celery==3.1.18
$ pip freeze > requirements.txt

Now it is time to integrate Celery into our online shop project:
Step 1: Add celery.py
Inside the “onlineshop” directory, create and write in a new file called celery.py as shown in the project.
Step 2: Import your new Celery app
To ensure that the Celery app is loaded when Django starts, add the following code into the __init__.py file that sits next to your settings.py file:
from __future__ import absolute_import

# This will make sure the app is always imported when
# Django starts so that shared_task will use this app.
from .celery import app as celery_app

Having done that, your project layout should now look like:
├── manage.py
├── onlineshop
│   ├── __init__.py
│   ├── celery.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── requirements.txt
Step 3: Install Redis as a Celery “Broker”
Celery uses “brokers” to pass messages between a Django project and the Celery workers. In this tutorial, we will use Redis as the message broker.
First, install Redis from the official download page or via brew (brew install redis) and then turn to your terminal, in a new terminal window, fire up the server:
$ redis-server

You can test that Redis is working properly by typing this into your terminal:
$ redis-cli ping

Redis should reply with PONG - try it!
Once Redis is up, add the following code to your settings.py file:
# CELERY STUFF
BROKER_URL = 'redis://localhost:6379'
CELERY_RESULT_BACKEND = 'redis://localhost:6379'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = 'Africa/Nairobi'

You also need to add Redis as a dependency in the Django Project:
$ pip install redis==2.10.3
$ pip freeze > requirements.txt

Done! It is now possible to use Celery with Django. For further information on Celery settings with Django, please check out the official Celery documentation.

