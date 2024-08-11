---
up:
  - "[[Flask]]"
related: 
created: 2024-07-25
---
- الأكواد الغريبة اللي كتبناها في [[Create And Extends HTML Templates Flask]] عشان نعمل extend اسمها Jinja template
- يستحسن تنزلها extension تساعدك فالكود
- [Template Designer Documentation — Jinja Documentation (2.10.x)](https://jinja.palletsprojects.com/en/2.10.x/templates/)
- دي بتساعدني باختصار عشان أستخدم الأكواد العادية مع الـ Python في صفحات الـ Webpage وعشان أعمل Template يكون بيتغير 

There are a few kinds of delimiters. The default Jinja delimiters are configured as follows:

- `{% ... %}` for [Statements](https://jinja.palletsprojects.com/en/2.9.x/templates/#list-of-control-structures)
- `{{ ... }}` for [Expressions](https://jinja.palletsprojects.com/en/2.9.x/templates/#expressions) to print to the template output
- `{# ... #}` for [Comments](https://jinja.palletsprojects.com/en/2.9.x/templates/#comments) not included in the template output

## Use Attributes
- اتكلمنا عنها قبل كدا في [[Create HTML Files and use variables - Flask#Use attributes|Use attribute]]
- تقدر تسمي الـ Attribute أي حاجة وتقدر تستخدمه فأي حته في فايل الـ HTML
```python
from flask import Flask, render_template

skills_app = Flask(__name__)

@skills_app.route("/")
def homepage():
  return render_template("homepage.html", title="Homepage", test="test")

@skills_app.route("/about")
def about():
  return render_template("about.html", title="About Us", test="test")

if __name__ == "__main__":
  skills_app.run(debug=True, port=9000)
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>{{ title }}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}" />
    <link rel="stylesheet" href="{{ url_for('static', filename='css/master.css') }}" />
  </head>
  <body>
	  {{ test }}
	  {% block body %}
	  {% endblock %}
  </body>
</html>
```

- خد بالك الـ variable بتبقا {{ }} انما لو بعمل template بتبقا {% %}
## Use CSS files
- في الـ Template لازم استخدمها بطريقة مختلفة شوية
```plain-text
{{ url_for('static', filename="css/main.css")}}
```

- هتعمل folder اسمه static وتحط جواه الـ CSS و JS
- اعمله جنب الـ templates، لو مغيرتش اعدادات الـ Flask هيروح يدور عليها

## If condition 
- ممكن لما تيجي تستخدم الـ Attributes دي فالـ body يحصل مشاكل زي إني في صفحة من الصفحات محطش الـ Attribute 
- هو لو في div أو حاجة بيظهر فاضي وبيبقا شكله وحش

```html
{% if custom_css %}
<div> {{ custom_css }}
{% endif %}

```

## Use if with CSS
- لو أنا عايز كل صفحة يبقا ليها CSS فايل مختلف وممكن حاجة منهم ميبقاش ليها فايل
- هنعمل Variable جديد ونستخدمه في الربط

```python
from flask import Flask, render_template

skills_app = Flask(__name__)

@skills_app.route("/")
def homepage():
  return render_template("homepage.html",
                          title="Homepage",
                          custom_css="home")
@skills_app.route("/add")
def add():
  return render_template("add.html",
                          title="Add Skill",
                          custom_css="add")

@skills_app.route("/about")
def about():
  return render_template("about.html", title="About Us")

if __name__ == "__main__":
  skills_app.run(debug=True, port=9000)
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>{{ title }}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}" />
    <link rel="stylesheet" href="{{ url_for('static', filename='css/master.css') }}" />
    {% if custom_css %}
    <link rel="stylesheet" href="{{ url_for('static', filename='css/' + custom_css + '.css') }}" />
    {% endif %}
  </head>
  <body>
    {% block body %}
    {% endblock %}
  </body>
</html>
```
- هنعمل Concatenate بين الـ Variable والـ  Text عشان فالآخر يطلعلي المسار بتاع الفايل صح

## For Loop
- نفترض إن عندي List of Tuples وعايز أظهرها 

```python
my_skills = [("Html", 80), ("CSS", 75), ("Python", 95)]

@skills_app.route("/skills")
def skills():
  return render_template("skills.html",
                          title="My Skills",
                          page_head="My Skills",
                          description="This Is My Skills Page",
                          skills=my_skills)
```

```html
{% extends 'base.html' %}
{% block body %}
<h1 class="page-head">{{ page_head }}</h1>
<p class="page-description">{{ description }}</p>

{% for skill in skills %}
<div>
  {{ skill[0] }} | {{ skill[1] }}
</div>
{% endfor %}

{% endblock %}
```