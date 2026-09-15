## Flask Application Object

A flask application object is an instance of the Flask class that represents your web application. It holds configuration, the URL map (routes), template settings and serves as the central registry for everything your app does.

- The application object is the brain of your app. Every route, config setting, and extension attaches it.

## Flask Constructor

- The Flask Constructor is Flask(import_name). Its required argument is the name of the module or package in which the application is defined.
- Flask uses this to locate templates, static files, and other resources relative to the application's root path.

```python
from flask import Flask

app = Flask(__name__)
```
### Why __name__?
- __name__ is a special python variable that holds the name of the current module.
 1. Script run directly (`python app.py`) `"__main__"`
 2. Module imported (`import app`) -> `"app"`

When you pass `__name__` to Flask(), Flask uses it to determine where the application root is -- so it can find `templates/`, `static/` and config files relative to that location.

## View Function
A view function is a Python function that handles an HTTP request and returns an HTTP response. In Flask, view functions are mapped to URLs via the routing system.
1. A view function is just a function that runs when someone visits a certain URL. It receives the request (optionally) and returns what the browser should see.
## Routing
Routing is the mechanism by which a web framework maps a URL pattern to a view function. When an HTTP request arrives, the framework matches its path against the registered routes and dispatches to the corresponding view.

```python
@app.route("/path")
def function_name():
    return "response"
```

#### What happens step-by-step
1. Python reads `@app.route("/path")` before defining the function.
2. The decorator calls `app.route("/path")`, which returns a decorator function.
3. That decorator receives `function_name` and registers it in `app.url_map` with the URL `/path`
4. The original function is returned unchanged (and bound to function_name).
5. 1. Later, when a request for `/path` arrives, Flask looks up the URL in `url_map`, finds `function_name`, and calls it.

## Development Server
The **development server** is a lightweight HTTP server bundled with Werkzeug (Flask's underlying library), intended for local development and testing only. It is not designed for production use.
## Returning Different Response Types

Flask view functions can return several things:

### 1. A string (most common)

```python
@app.route("/text")
def text():
    return "Plain text response"
```
### 2. A tuple: `(body, status_code)`

```python
@app.route("/custom-status")
def custom_status():
    return "Resource created", 201
```

### 3. A tuple: `(body, status_code, headers)`
```python
@app.route("/with-headers")
def with_headers():
    return "Cached", 200, {"Cache-Control": "max-age=3600"}
```

### 4. A `Response` object (explicit control)
```python
from flask import Response
@app.route("/response-object")
def response_object():
    return Response("Custom response", status=200, mimetype="text/plain")
```

### 5. JSON (via `jsonify`)
```python
from flask import jsonify
@app.route("/api/user")
def api_user():
    return jsonify({"name": "Alice", "age": 30})
```

**Formal definition: `jsonify`**

> `jsonify()` is a Flask helper that serializes Python data (dicts, lists) into a JSON HTTP response with the correct `Content-Type: application/json` header.
## The Complete Flow of a Request (Formal)

Let's trace what happens when you visit `http://127.0.0.1:5000/about`:

1. **Browser** sends:
    
    text
    
    GET /about HTTP/1.1
    Host: 127.0.0.1:5000
    
2. **Werkzeug** (the WSGI server) receives the raw request and converts it into a WSGI environment dictionary.
    
3. **Flask** wraps that into a `Request` object.
    
4. Flask's **URL map** matches `/about` to the `about` endpoint.
    
5. Flask calls the `about()` view function.
    
6. The view returns `"This is the about page."`.
    
7. Flask converts this to a `Response` object with status `200` and MIME type `text/html`.
    
8. **Werkzeug** serializes the response back to HTTP and sends it to the browser.
    
9. The **browser** renders the text.
    

This entire process is called the **request–response cycle**.