Django setup
---
in terminal:
`pip3 install 'django<4' gunicorn`
`pip3 install dj_database_url==0.5.0 psycopg2`
`pip3 install dj3-cloudinary-storage`

After setups and installment, run in terminal:
`pip3 freeze --local > requirements.txt`

To create Django project, run in terminal:
`django-admin startproject axolothblog .`

To create app, run in terminal:
`python3 manage.py startapp blog`

For every app created, add it to the settings list, then migrate. In terminal:
`python3 manage.py makemigrations`
`python3 manage.py migrate`