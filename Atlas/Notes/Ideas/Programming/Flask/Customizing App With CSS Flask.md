---
up:
  - "[[Flask]]"
related: 
created: 2024-07-26
---


- بكل بساطة لو عايز أعمل مثلًا bar بيتغير على حسب الـ Progress بتاعي مثلًا 
- هنستخدم الـ Inline style 

```python
# ---------------------------------------
# -- Flask => Customizing App With Css --
# ---------------------------------------

from flask import Flask, render_template

skills_app = Flask(__name__)

my_skills = [("Html", 80), ("CSS", 75), ("Python", 95), ("MySQL", 45)]

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

@skills_app.route("/skills")
def skills():
  return render_template("skills.html",
                          title="My Skills",
                          page_head="My Skills",
                          description="This Is My Skills Page",
                          skills=my_skills,
                          custom_css="skills")

if __name__ == "__main__":
  skills_app.run(debug=True, port=9000)
```

```html
{% extends 'base.html' %}
{% block body %}
<h1 class="page-head">{{ page_head }}</h1>
<p class="page-description">{{ description }}</p>

{% for skill in skills %}
<div class="skill-box">
  <div class="skill-name">{{ skill[0] }}</div>
  <div class="skill-progress">
    <span style="width: {{ skill[1] }}%"></span>
  </div>
</div>
{% endfor %}

{% endblock %}
```

`main.css`
```css
* {
  box-sizing: border-box
}
body {
  background-color: #EEE;
  font-family: Arial, Tahoma;
}
.page-head,
.page-description {
  text-align: center;
}
.page-head {
  font-size: 40px;
  margin: 20px 0 0;
}
.page-description {
  font-size: 22px;
  margin: 10px 0 40px;
}
```

`skills.css`
```css
.skill-box {
  background-color: #FFF;
  padding: 20px;
  margin: 20px auto;
  border: 1px solid #CCC;
  width: 450px;
}
.skill-box .skill-name {
  text-align: center;
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: bold;
}
.skill-box .skill-progress {
  background-color: #F7F7F7;
  padding: 10px;
  position: relative;
}
.skill-box .skill-progress span {
  position: absolute;
  left: 0;
  top: 0;
  width: 0;
  height: 100%;
  background-color: #009688
}
```