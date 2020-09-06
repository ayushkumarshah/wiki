
# Create login and registration forms

## 1. Create `forms.py`

```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField, BooleanField
from wtforms.validators import DataRequired


class LoginForm(FlaskForm):
    email = StringField("Email", validators=[DataRequired()])
    password = PasswordField("Password", validators=[DataRequired()])
    remember_me = BooleanField("Remember me")
    submit = SubmitField("Login")

class RegisterForm(FlaskForm):
    
    email = StringField("Email", validators=[DataRequired()])
    password = PasswordField("Password", validators=[DataRequired()])
    password_confirmed = PasswordField("Confirm Password", validators=[DataRequired()])
    first_name = StringField("First name", validators=[DataRequired()])
    last_name = StringField("Last name", validators=[DataRequired()])
    submit = SubmitField("Register now")
```

## 2. Update login route and login template

### Login route

```python
@app.route("/login", methods=['GET', 'POST'])
def login():
    form = LoginForm()
    return render_template("login.html", title="Login", form=form, login=True)
```

### Login template `login.html`

```html
    {% extends "layout.html" %}
   
    {% block content %}
    <h1>{{title}}</h1>

    <div class="row">
        <div class="col-md-6 offset-md-3">
            <h3></h3>
            <form name="login" action="" method="post">
              {{ form.hidden_tag() }}
              <p>
                {{ form.email.label }}<br>
                {{ form.email(size=35) }}
              </p>

              <p>
                {{ form.password.label }}<br>
                {{ form.password(size=35) }}
              </p>
              <p>
                {{ form.submit()}}
              </p>
            </form>
        </div>
    </div>
 {% endblock %}
```

