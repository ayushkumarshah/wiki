
1. Setup virtual environment

```console
$ virtualenv venv
$ source venv/bin/activate
```

2. Install flask and flask-wtf (for forms)

```console
$ pip install flask flask-wtf
```

3. Set environment

```console
vim .flaskenv
```

Add these lines
```env
FLASK_ENV = development
FLASK_APP = main.py
```

4. Install package for form

```console
$ pip install python-dotenv
```

5. Create main.py

```python
app = Flask(__name__) # special ariable to identify the current application or module being rendered or passed to flask.
@app.route("/")

@app.route("/index")
def index():
    return "<h1>Hello!!</h1>"
```

6. Run the app
```console
flask run
```
