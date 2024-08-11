---
up:
  - "[[Flask]]"
related: 
created: 2024-07-25
---
It's micro (note that)

---
## Installing
```sh
pip install flask
flask --version
```

## Make virtual env
```sh
pip3 install virtualenv
python -m venv name_of_folder
```
## First page

```python
# import it
from flask import Flask

# Give name
skills_app = Flask(__name__)
```

## route
```python
@skills_app.route("/") # مسار الصفحة الرئيسية
# Return Information for this route or path
def homepage():
	return"Hello Corn, It's home page"

@skills_app.route("/about")
def about():
	return "It's about page"

@app.route('/user/<username>')
def profile(username):
    return f'{username}\'s profile'
```

We can add two routes for same function
```python
@app.route('/about/', strict_slashes=False)
@app.route('/about/<text>', strict_slashes=False)
def python(text='is cool'):
    text = text.replace('_', ' ')
    return f'Python {text}'
```
### strict slashes
- هي عبارة عن option وانت موجود وانت بتعرف الـ Route بتحدد الـ slash هيفرق ولا لا في الـ URL
- By default, it's `True`, meaning that `/path` and `/path/` are considered different routes.
- Setting `strict_slashes=False` makes Flask treat `/path` and `/path/` as identical, allowing both to match the same route.

#### How to use it
You can set `strict_slashes=False` either globally or for specific routes:
```python
from flask import Flask

app = Flask(__name__)
app.url_map.strict_slashes = False

@app.route('/users')
def users():
    return 'Users page'
```

**For a specific route:**
```python
from flask import Flask

app = Flask(__name__)

@app.route('/products', strict_slashes=False)
def products():
    return 'Products page'
```
#### Why use it?

There are several reasons to use `strict_slashes=False`:

- **SEO:** Search engines often treat URLs with and without trailing slashes differently, which can lead to duplicate content issues. By using `strict_slashes=False`, you ensure that both versions point to the same content, improving your SEO.
- **User experience:** Users might accidentally type a trailing slash, and without `strict_slashes=False`, they would be redirected to a 404 error.
- **Development convenience:** It simplifies route definition by not having to worry about trailing slashes.

### Variable Rules

You can add variable sections to a URL by marking sections with `<variable_name>`. Your function then receives the `<variable_name>` as a keyword argument. Optionally, you can use a converter to specify the type of the argument like `<converter:variable_name>`.

```python
from markupsafe import escape

@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return f'User {escape(username)}'

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return f'Post {post_id}'

@app.route('/path/<path:subpath>')
def show_subpath(subpath):
    # show the subpath after /path/
    return f'Subpath {escape(subpath)}'
```

**Converter types:**

| type | explain|
|-------|----------|
|`string`|(default) accepts any text without a slash|
|`int`| accepts positive integers|
|`float`| accepts positive floating point values|
|`path`| like `string` but also accepts slashes|
|`uuid`|accepts UUID strings|
## run

```python
# Run the page only when run it directly
if __name__ == "__main__":
	skills_app.run()
```
We talked about it at [[Py __name__ and __main__]]

---
The debugger is off by default, you should active it when you run it
```python
skills_app.run(debug=True)
```

Also we can change port, If you work at another port
```python
skills_app.run(port=9000)
```

Also we can change host

```python
skills_app.run(host='0.0.0.0')
```

- **`host='0.0.0.0'`:** Listens on all available interfaces.
- **`host='127.0.0.1'`:** Listens only on the local loopback interface (localhost).

الفرق بين الـ Port والـ IP إن الـ IP هيوصلك للجهاز بس انت مش عارف الـ Application فالبورت زي العنوان بتاع الـ Application