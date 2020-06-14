# Creating sessions and 

- Make data active across multiple pages
- Flask-Session extension used
- Implementation on top of cookies and signs cookies crypotgraphically
- Code similar to PHP
- Session and state management using Flask-Login extension is 
  more secure and more interaction with the database

## Generate secret key

```console
python -c "import os; print(os.urandom(16))"
```

## Create Session for login

```python
    from flask import session
    @app.route("/login", methods=['GET', 'POST'])
    def login():
        if session.get('username'):
            return redirect(url_for('index'))
        ...
        ...

        if user and user.get_password(password):
        # if request.form.get("email") == "test@uta.com":
            flash("{}, You are successfully logged in".format(user.first_name), "success")
            session['user_id'] = user.user_id
            session['username'] = user.first_name
            return redirect("/index")

    def register():
        if session.get('username'):
            return redirect(url_for('index'))

```

## Create session for logout and enrollment routes

### Create logout route

```python
@app.route("/logout")
def logout():
    session['user_id'] = False
    session.pop('username', None)
    return redirect(url_for('index'))

```

### Update enrollment route to include user_id and also redirect to login page if not signed in

```python
@app.route("/enrollment", methods=["GET", "POST"])
def enrollment():

    # If not signed in, goto login page
    if not session.get('username'):
        return redirect(url_for('login'))
    courseID = request.form.get("courseID")
    courseTitle = request.form.get("title")
    user_id = session.get('user_id') 

```

## UPdate index page

```html
{% extends 'layout.html' %}

{% block content %}
<div class="row">
        <div class="col-md-12 text-center">
            <h1>Welcome to Universal Tech Academy.</h1>

            {% if session['username'] %}
            <h3>Let's get started.</h3>
            {% else %}
            <p>Already registered? <a href="{{url_for('login')}}">Login</a></p>
            
            {% endif %}
        </div>
    </div>

{% endblock %}
```

## UPdate nav bar

```html
    <header>
        <nav>
            <ul class="nav nav-pills">
              <li class="nav-item"><a href="{{ url_for('index') }}" class="nav-link {% if index %}active{% endif %}">Home</a></li>
                <li class="nav-item"><a href="{{ url_for('courses') }}" class="nav-link {% if courses %}active{% endif %}">Classes</a></li>
                {% if not session['username'] %}
                <li class="nav-item"><a href="{{ url_for('register') }}" class="nav-link {% if register %}active{% endif %}">Register</a></li>
                {% endif %}
                <li class="nav-item"><a href="{{ url_for('enrollment') }}" class="nav-link {% if enrollment %}active{% endif %}">Enrollment</a></li>
                {% if not session['username'] %}
                <li class="nav-item"><a href="{{ url_for('login') }}" class="nav-link {% if login %}active{% endif %}">Login</a></li>
                {% else %}
                <li class="nav-item"><a href="{{ url_for('logout') }}" class="nav-link">Logout</a></li>
                {% endif %}
            </ul>
        </nav>
        <hr style="clear:both">
    </header>

```


## Add welcome message in `layout.html`

```html

  {% include "includes/nav.html" %}

  {% if session['username'] %}
  <span class="user">Welcome, {{ session['username'] }}</span>
  {% endif %}

```
