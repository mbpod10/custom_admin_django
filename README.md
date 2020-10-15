# Customize Django Admin

For and foremost, we need to make the django project, app, and superuser

```
django-admin startproject <PROJECT_NAME>
django-admin startapp <APP_NAME>
cd <PROJECT_NAME>
python3 manage.py createsuperuser
```

Go to http://127.0.0.1:8000/admin/ and login

### HTML Customize

We need to make an `admin` directory within the `templates` folder within our root project. The subsequent files that go into this folder need to be exactly the same as the django repo on GitHub. We are going to change the HTML within these files.

- Go to https://github.com/django/django/blob/master/django/contrib/admin/templates/admin/base_site.html to change the `base_site.html` file. The Django repo contains all the templates you need to customize the HTML of the admin.
- Here we can change the title of the admin HTML page.

```html
{%extends "admin/base.html"%} {%block title%}{%if subtitle%}{{subtitle}} |
{%endif%}{{ title }} | {{ site_title|default:_('Django site admin')}}
{%endblock%} {% block branding %}
<h1 id="site-name">
  <a href="{% url 'admin:index' %}">VIDEO STORE ADMIN</a>
</h1>
{% endblock %} {% block nav-global %}{% endblock %}
```

We changed the Title to 'VIDEO STORE ADMIN'

- go back to http://127.0.0.1:8000/admin/ and the admin title is changed

### Create Models

After creating your models such as:

```python
from django.db import models

class Movie(models.Model):
    title = models.CharField(max_length=256)
    length = models.PositiveIntegerField()
    release_year = models.PositiveIntegerField()

    def __str__(self):
        return self.title


class Customer(models.Model):
    first_name = models.CharField(max_length=256)
    last_name = models.CharField(max_length=256)
    phone = models.PositiveIntegerField()

    def __str__(self):
        return self.first_name + " " + self.last_name

```

Then go to `admin.py` in <PROJECT_NAME> and hook up your models with the admin site

```python
from django.contrib import admin
from . import models

admin.site.register(models.Customer)
admin.site.register(models.Movie, MovieAdmin)

```

Go back to http://127.0.0.1:8000/admin/ to make sure models are viewed

### Admin Views
