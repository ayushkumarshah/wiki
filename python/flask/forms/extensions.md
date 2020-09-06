# Extensions

## 1. Flask-WTF extension

```console
pip install flask-wtf
```
- extension for the WTForms library
- allows to create html forms
- maintains separation of code and presentation (similar to MVC)
- Jinja template system

WTForms

```html
<form>
{{ from.hidden_tag() }}
{{ from.username  }}
...
...
</form>
```

Standard HTML Form

```html
<form>
<input id="csrf_token"
type="hidden"
name="scrf_token"
value="ImSSSSSdfmm..Gu64nds3"
<input tpe="text" name="username">
...
...
</form>
```

> hidden tag function - special function to generate csfr_token (cross side request forge token). 
> It ensures form submitted to site is secure

## 2. Flask-security Extension

```console
pip install flask-security
```

- Session based authentication
- Password hashing
- Basic HTTP and token based authentications
- User registration
- Login tracking (Flask-login)
- Data persistency for Flask-SQLAlchemy, Flask-MongoEngine, flask-peewee, PonyORM

