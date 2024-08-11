---
up:
  - "[[Flask]]"
related: 
created: 2024-07-25
---
We can use [[HTML-CSS]] at flask

To use it, we should use `render_template`

```python
from flask import Flask, render_template

skills_app = Flask(__name__)

@skills_app.route("/")
def homepage():
	return render_template("homepage.html")
	# html file will be rendered
	# It should be founded

@skills_app.route("/about")
def about():
  return render_template("about.html", pagetitle="About Us")

if __name__ == "__main__":
  skills_app.run(debug=True, port=9000)
```

## Use Variables
- تقدر تتحكم في صفحة الـ HTML بتاعتك من خلال الـ Flask عن طريق إنك بتديله زي Attribute وبتحط القيمة بتاعته وهو بيحطها مكانه

```python
@skills_app.route("/")
def homepage():
	return render_template("homepage.html", pagetitle="H")
```

- مش هتأثر لحد دلوقتي، لحد ما نستخدم الـ Attribute دا في الـ HTML
```html
<!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>{{ pagetitle }}</title> # used here 
  </head>
  <body>
    Hello From Home Page
  </body>
</html>
```

هنستخدم الحوار دا عشان في الـ HTML نفسه مش هنعدل غير على فالـ body بتاعنا 