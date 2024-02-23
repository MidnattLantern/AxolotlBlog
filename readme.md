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

Cloudinary
---
- As of 20 feb 2024, the API enviroment variable is found inside "programmable media"
- Add to the env.py:
`os.environ["CLOUDINARY_URL"]=`
- Add to installed apps:
`
cloudinary_storage
cloudinary
`
- Add underneath STATIC_FILES:
`
STATICFILES_STORAGE = 'cloudinary_storage.storage.StataicHashedCloudinaryStorage'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

MEDIA = '/media/'
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
`
- Add underneath BASE_DIR:
`
TEMPLATES_DIR = os.path.join(BASE_DIR, 'templates')
`
- Add inside the empty array 'DIRS' []:
`TEMPLATES_DIR`
- media, templates, and static folder was added in the base directory.


Heroku (manual method):
---
- In settings.py, add `axolotl-blog-66ea1f84b437.herokuapp.com` to allowed hosts. It may be neccessary to update this link. Without this, it won't be possible to deploy.
- Heroku need a Procfile to read the repository. Add this in Procfile:
`
web: gunicorn axolotlblog.wsgi
`
- In Heroku, Create a new Heroku app.
- In the settings tab, add keys and values, the same as from your env.py file.
- Add the key: "DISABLE_COLLECTSTATIC" and the value: "1". Without this, the deployment will fail.
- When deploying for the first time, make sure the app is connected to the GitHub repository.
- For each deployment, make sure the git repository is commited to date, and that the requirements are frozen.


Summernote:
---
- In terminal:
`pip3 install django-summernote`
- Freeze:
`pip3 freeze --local > requirements.txt`
- Add to installed apps


Allauth:
---
- In terminal:
`pip3 install django-allauth`
- Add to urls.py inside axolotlblog:
`path('accounts/', include('allauth.urls')),`
- Add to installed apps:
`
allauth
django.contrib.sites
allauth.account
allauth.socialaccount
`

crispy forms
---
- In terminal:
`pip3 install django-crispy-forms==1.14.0`
- Don't forget to freeze and add to installed apps:
`crispy_forms`
- This need to be added too:
`CRISPY_TEMPLATE_PACK = 'bootstrap4'`


blog.py models
---
`Import User`
`import CloudinaryField` enable the use of Cloudinary, the cloud platform service hosting images.
CASCADE: With one-to-many fields, a records and all its content wants to be deleted.


admin.py
---
`prepopulated_fields = {'slug': ('title',)}` automatically generates a slugfield when editing from the admin panel. This will only work when working inside the admin panel.


Etc
---
`ACCOUNT_EMAIL_VERIFICATION = 'none'` in settings.py prevent 500 error
- This works with allauth, so that you're sent to the main page when log in or out:
`
SITE_ID = 1
LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'
`
- To see the version of Python, run this in terminal:
`ls ../.pip-modules/lib`
- add this for each form:
`{% csrf_token %}`