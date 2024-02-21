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


ElephantSQL setup
---
- At the top corner, select "create new instance".
- Axoloth Blog use tiny turtle plan.
- Click "Select region". Axolotl Blog use Stockholm.
- Click "Review", then "Create Instance".
- When entering Axoloth Blog, there's a URL section and a copy button icon. This will be used in the env.py file.
- The env.py with postgreSQL shoudl look like this: `os.environ["DATABASE_URL"]="(copied url)"`
- In settings.py disable the default databse code, and use this instead:
`
DATABASES = {
    'default': dj_database_url.parse(os.environ.get("DATABASE_URL"))
}
`
- Back at ElephantSQL, click Browse, select "auth_user_public" on the list, then execute.

env.py
---
- Don't forget to make sure env.py is listed in the .gitignore file
- Add this block in settings.py below "Path":
`
import os
import dj_database_url
if os.path.isfile('env.py'):
    import env
`
- Replace the secret key with this:
`= os.environ.get('SECRET_KEY')`