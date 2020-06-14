# Working with Flask REST APIs

## 1. Install FLask-RESTPlus API Extension

```console
$ pip install flask-restplus
```

### Features

- support for creating REST APIs
- minimal setup
- provides colleciton of decorators and tools to describe APIs
- Multiple endpoitns allowed in the route() decorator
- Built in support for request data validation

## 2. Install Postman

### Features

- API development environment for testing APIs
- Chrome's HTTP client (Chrome extension available)
- Automate testing with Collection runner
- API Monitoring



## 3. Create API

|Request|Operation|Description|
|---|---|---|
|POST|CREATE|Insert data|
|GET|READ|Fetch data|
|PUT|UPDATE|Replace Existing data|
|DELETE|Delete|Remove data|

### Fetch data using GET

#### Add Api library in `__init__.py`

```python
from flask_restplus import api

api = api()
app = flask(__name__)
app.config.from_object(config)

db = mongoengine()
db.init_app(app)

api.init_app(app)

from app import routes
```

#### Create API in routes

`routes.py`

```python
from app import Api
from flask_restplus import Resource

#####################################################

@api.route('/api', '/api/')
class GetAndPost(Resource):

    def get(self):
        return jsonify(User.objects.all())



@api.route('/api', '/api/<idx>')
class GetUpdateDelete(Resource):

    def get(self, idx):
        return jsonify(User.objects(user_id=idx))

###################################################

```

### Write data using POST

```python
# POST
def post(self):
   
    data = api.payload

    user = User(user_id=data['user_id'], email=data['email'], 
                first_name=data['first_name'], last_name=data['last_name'])
    user.set_password(data['password'])
    user.save()
    return jsonify(User.objects(user_id=data['user_id']))
```

Add JSON data in postman using post request

### UPdate data using PUT

```python
# PUT
def put(self, idx):
    data = api.payload
    User.objects(user_id=idx).update(**data)
    return jsonify(User.objects(user_id=idx))
```

### Delete data using DELETE

```python
# DELETE
def delete(self, idx):
    User.objects(user_id=idx).delete()
    return jsonify("User is deleted")
```
