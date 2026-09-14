## Web Development
Web development is the process of building and maintaining applications that communicate over the World Wide Web using the HTTP protocol, typically following the client-server architecture.

## HTTP (HyperText Transfer Protocol)
HTTP is an application layer protocol used for transmitting hypermedia documents (like HTML) over the internet. It defines how messages are formatted and transmitted, and how servers and browsers should respond to various commands.
- Every HTTP has two parts:
- **A. HTTP Request**: An HTTP request is a message sent by a client to a server for a resource or action.
- **Common HTTP Methods:**

| Method   | Definition                  | Purpose          |
| -------- | --------------------------- | ---------------- |
| `GET`    | Retrieve a resource         | View a page      |
| `POST`   | Submit data to be processed | Submit a form    |
| `PUT`    | Replace a resource entirely | Update a record  |
| `PATCH`  | Partially modify a resource | Update one field |
| `DELETE` | Remove a resource           | Delete a record  |
**B. HTTP Response:** An HTTP Response is a message sent by a server to a client containing the result of the request.
**Common HTTP Status Codes:**

|Code|Meaning|
|---|---|
|`200 OK`|Success|
|`201 Created`|Resource created|
|`301 / 302`|Redirect|
|`400 Bad Request`|Client sent invalid data|
|`401 Unauthorized`|Authentication required|
|`403 Forbidden`|Authenticated but not allowed|
|`404 Not Found`|Resource doesn't exist|
|`500 Internal Server Error`|Server crashed|
## FLASK

- Flask is a lightweight, WSGI-compliant micro web framework for Python.
- It provides the essential tools for building web applications - routing, request handling, templating while leaving decisions about databases, authentication, and other concerns to a developer.
- ### Breaking That Down:

|Term|Definition|
|---|---|
|**Micro framework**|Provides a minimal core. Does not enforce a specific project layout or include an ORM/admin panel by default.|
|**WSGI-compliant**|Follows the **Web Server Gateway Interface**, a standard Python specification for how web servers communicate with web applications.|
|**Extensions**|Third-party packages that add features (e.g., `Flask-SQLAlchemy`, `Flask-Login`).|
### Flask's Core Components:

1. **Routing system** — maps URLs to Python functions
    
2. **Request/Response objects** — wrap HTTP data
    
3. **Jinja2 template engine** — generates HTML dynamically
    
4. **Werkzeug** — the underlying WSGI toolkit (URL parsing, HTTP utilities)
    
5. **Session support** — signed cookies for state

## WSGI (Web Server Gateway Interface)

WSGI is a Python specification (PEP 3333) that defines a standard interface between web servers and Python web applications, allowing any WSGI-compliant application to run on any WSGI-compliant server.

**Why it matters:**

- Flask apps are WSGI applications.
    
- You can run the same Flask app on Gunicorn, uWSGI, or Waitress without changing code.
    
- In development, Flask uses **Werkzeug's development server**; in production, you use a real WSGI server.

## Decorators in Python
A **decorator** is a function that takes another function and returns a modified version of it, using the `@decorator` syntax.

```python
def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Before
# Hello!
# After
```

### In flask
```python
@app.route("/")
def home():
    return "Hello"
    
`@app.route("/")` is a decorator that registers home() as the handler for the URL `/`.
```

## URL DISPATCHING OR ROUTING

Flask maintains a URL map - a mapping from URL patterns to Python view functions. When a request arrives, Flask matches the URL against this map and calls the corresponding function.

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Home page"

@app.route("/about")
def about():
    return "About page"
```
When the browser requests `/about`:

1. Flask receives the HTTP request.
    
2. It looks up `/about` in its URL map.
    
3. It finds `about()` and calls it.
    
4. The returned string becomes the HTTP response body.
    
5. Flask sends back `200 OK` with that body.