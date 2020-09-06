1. Install mongodb

```console
brew tap mongodb/brew
brew install mongodb-community@4.2
```
> To run MongoDB (i.e. the mongod process) as a macOS service, issue the following:

```
brew services start mongodb-community@4.2
```

> To run MongoDB (i.e. the mongod process) manually as a background process, issue the following:

```
mongod --config /usr/local/etc/mongod.conf --fork
```

2. Install flask-mongoengine

```console
pip install flask-mongoengine
```

3. Setup database settings

`__init__.py`

```python
from config import Config
from flask_mongoengine import MongoEngine


app = Flask(__name__)
app.config.from_object(Config)

db = MongoEngine()
db.init_app(app)
```

`config.py`

```python

import os


class Config(object):

    SECRET_KEY = os.environ.get("SECRET_KEY") or "secret_string"

    MONGODB_SETTINGS = { 'db': 'UTA_Enrollment',
                        'host': 'mongodb//localhost:27017/UTA_Enrollment'
                        }
    # host is optiona
```

4. Connecting flask to database

- Add class and route

  ```python

  class User(db.Document):
      user_id = db.IntField(unique=True)
      first_name = db.StringField(max_length=50)
      last_name = db.StringField(max_length=50)
      email = db.StringField(max_length=30)
      password = db.StringField(max_length=30)

  @app.route("/user")
  def user():
      User(user_id=1, first_name="Ayush", last_name="Shah", 
           email="ayush.kumar.shah@gmail.com", password="1234").save()
      User(user_id=2, first_name="Bibash", last_name="Shrestha", 
           email="bibash@gmail.com", password="12345").save()
      User(user_id=3, first_name="Kamlesh", last_name="Kunwar", 
           email="kamlesh@gmail.com", password="01234").save()
      users = User.objects.all()
      return render_template("users.html", users=users)

  ```

- Displaying in `users.html`

  ```html

  {% extends 'layout.html' %}

  {% block content %}
  <div class="row">
          <div class="col-md-12 text-center">
          
            {% for user in users %}
            <d1>
              <dt>User ID: {{ user.user_id }</dt>}
              <dd>Email: {{ user.email }</dd>}
              <dd>Password: {{ user.password }</dd>}
            </d1>
            {% endfor %}
          </div>
      </div>

  {% endblock %}

  ```

5. Creating documents and data
```python
db.createCollection(<collection>)
db.<collection>.insert({..})
db.<collection>.insertMany({..})
```

6. Import data from json to mongo

```console
mongoimport --db UTA_Enrollment --collection user --jsonArray --file data/users.json
```

### Common mongo comands
```console
mongo
```

```mongo
show databases
use database_name
show collections
db.collection_name.find()
db.collection_name.drop()
```

