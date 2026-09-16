## URL (Uniform Resource Locator)
A URL is a reference to a web resource that specifies its location on a network and the mechanism for retrieving it.
## Anatomy of a URL:

```text
https://example.com:8080/users/42?sort=name#section1
└─┬─┘   └────┬────┘└┬─┘└───┬───┘└────┬────┘└───┬───┘
scheme    host    port   path    query   fragment
```


| Component    | Definition             | Example     |
| ------------ | ---------------------- | ----------- |
| **Scheme**   | Protocol               | https       |
| **Host**     | Domain or IP           | example.com |
| Port         | Communication endpoint | 8080        |
| Path         | Resource Location      | /users/42   |
| Query String | Key-value parameters   | ?sort=name  |
| Fragment     | Client-side anchor     | `#section1` |
**In Flask, `@app.route()` matches the _path_ (plus optional query parameters accessible via `request.args`).**
## URL Rule

> A **URL rule** is a string pattern registered with Flask that describes the structure of a URL path. It may contain **static parts** (literal text) and **dynamic parts** (variable segments enclosed in angle brackets).
### Examples:

|URL Rule|Matches|Doesn't Match|
|---|---|---|
|`/`|`/`|`/about`|
|`/about`|`/about`|`/About`, `/about/`|
|`/user/<username>`|`/user/alice`, `/user/bob123`|`/user/`, `/user/a/b`|
|`/post/<int:id>`|`/post/1`, `/post/999`|`/post/abc`|
## Dynamic Segment/ variable rule

 A Dynamic segment (also variable rule or path parameter) is a portion of a URL rule enclosed in angle brackets <...> that captures part of the incoming URL and passes it as an argument to the view function.
 
 ```python
 @app.route("/user/<username>")
def show_user(username):
    return f"User: {username}"
 ```
### What happens:

1. Request: `GET /user/alice`
    
2. Flask matches `/user/<username>` and extracts `username = "alice"`.
    
3. Flask calls `show_user(username="alice")`.
    
4. View returns `"User: alice"`.
    

**By default, dynamic segments capture strings that do not contain `/`.**

## Request Object

The **request object** is a Flask global (technically a context-local proxy) that provides access to incoming HTTP request data: method, headers, query parameters, form data, cookies, files, and the request body.
### Importing
```python
from flask import request
```

### Accessing the method
```python
@app.route("/info", methods=["GET", "POST"])
def info():
    return f"Method: {request.method}"
```

### Accessing query parameters (?key = value):
```python
@app.route("/search")
def search():
    query = request.args.get("q", "nothing")
    return f"Searching for: {query}"
```

### Accessing form data (POST):
```python
@app.route("/login", methods=["POST"])
def login():
    username = request.form.get("username")
    return f"Logged in as {username}"
```

## Reverse Routing/ URL Building
Reverse routing (URL Building) is the process of generating a URL from an endpoint name and parameters, rather than hardcoding it. Flask provides `url_for()` for this.
### Why is it important?
1. **No hardcoded URLs** — change a route in one place, all links update.
    
2. **Handles special characters** — automatically escapes/encodes URL segments.
    
3. **Works with dynamic segments** — inserts parameters correctly.

### Syntax:
```python
from flask import url_for

url_for("endpoint_name", **parameters)
```

### Examples:
```python
from flask import Flask, url_for

app = Flask(__name__)

@app.route("/")
def home():
    return f"About page: {url_for('about')}"

@app.route("/about")
def about():
    return "About"

@app.route("/user/<username>")
def profile(username):
    return f"Profile of {username}"

@app.route("/links")
def links():
    return {
        "home": url_for("home"),
        "about": url_for("about"),
        "alice": url_for("profile", username="alice"),
    }
```

visit `/links` -> you'll get:
```python
{
  "home": "/",
  "about": "/about",
  "alice": "/user/alice"
}
```
## Redirect

> A **redirect** is an HTTP response instructing the client to make a new request to a different URL. It uses status codes `301` (permanent) or `302`/`303`/`307`/`308` (temporary).
### Formal definitions of redirect status codes:

|Code|Meaning|
|---|---|
|`301 Moved Permanently`|Permanent; browsers cache it|
|`302 Found`|Temporary (legacy; may change method)|
|`303 See Other`|Temporary; explicitly forces GET|
|`307 Temporary Redirect`|Temporary; preserves method|
|`308 Permanent Redirect`|Permanent; preserves method|
