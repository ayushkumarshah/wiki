
# Processing Form Data

## UPdate `models.py`

```python
from werkzeug.security import generate_password_hash, check_password_hash

class User(db.Document):
    user_id = db.IntField(unique=True)
    first_name = db.StringField(max_length=50)
    last_name = db.StringField(max_length=50)
    email = db.StringField(max_length=30, unique=True)
    password = db.StringField()

    def set_password(self, password):
        self.password = generate_password_hash(password)

    def get_password(self, password):
        return check_password_hash(self.password, password)

```

## Update `forms.py`

```python
from wtforms.validators import DataRequired, Email, Length, EqualTo, ValidationError
from app.models import User

class LoginForm(FlaskForm):
    email = StringField("Email", validators=[DataRequired(), Email()])
    password = PasswordField("Password", validators=[DataRequired(), Length(min=6, max=15)])
    remember_me = BooleanField("Remember me")
    submit = SubmitField("Login")

class RegisterForm(FlaskForm):
    
    email = StringField("Email", validators=[DataRequired(), Email()])
    password = PasswordField("Password", validators=[DataRequired(), Length(min=6, max=15)])
    password_confirmed = PasswordField("Confirm Password", validators=[DataRequired(), Length(min=6, max=15),
                                                                     EqualTo('password')])
    first_name = StringField("First name", validators=[DataRequired(), Length(min=2, max=55)])
    last_name = StringField("Last name", validators=[DataRequired(), Length(min=2, max=55)])
    submit = SubmitField("Register now")

    def validate_email(self, email):
        user = User.objects(email=email.data).first()
        if user:
            raise ValidationError("Email is already in use. Pick another one")
```

## Update login and register layouts

### login.html

```html
    {% extends "layout.html" %}
   
    {% block content %}

    <div class="row">
        <div class="col-md-6 offset-md-3">
            <h3></h3>
            <form name="login" action="" method="post" novalidate>
              <fieldset class="form-group">
                <legend>{{title}}</legend>
              {{ form.hidden_tag() }}
              <p>
                {{ form.email.label }}<br>
                {{ form.email(size=35) }}
                {% for error in form.email.errors %}
                  <span class="error-message">{{ error }}</span> 
                {% endfor %}
              </p>

              <p>
                {{ form.password.label }}<br>
                {{ form.password(size=35) }}
                {% for error in form.password.errors %}
                  <span class="error-message">{{ error }}</span> 
                {% endfor %}
              </p>
              <p>
                {{ form.submit()}}
              </p>
            </form>
        </div>
    </div>
 {% endblock %}


```

### register.html
```html

    {% extends "layout.html" %}
   
    {% block content %}
    
    <div class="container">
         <form name="login" action="" method="post" novalidate>
        <fieldset class="form-group">
            <legend>{{title}}</legend>     
            {{ form.hidden_tag() }}       
                <p> {{ form.email.label }}</br>
                    {{ form.email }}
                    {% for error in form.email.errors %}
                     <span class="error-message">{{ error }}</span>
                    {% endfor %}
                </p>
            
                <p> {{ form.password.label }}</br>
                    {{ form.password }}
                    {% for error in form.password.errors %}
                     <span class="error-message">{{ error }}</span>
                    {% endfor %}
                </p>
            
                <p> {{ form.password_confirm.label }}</br>
                    {{ form.password_confirm }}
                    {% for error in form.password_confirm.errors %}
                     <span class="error-message">{{ error }}</span>
                    {% endfor %}
                </p>
            
                <p> {{ form.first_name.label }}</br>
                    {{ form.first_name }}
                    {% for error in form.first_name.errors %}
                     <span class="error-message">{{ error }}</span>
                    {% endfor %}
                </p>
            
                <p> {{ form.last_name.label }}</br>
                    {{ form.last_name }}
                    {% for error in form.last_name.errors %}
                     <span class="error-message">{{ error }}</span>
                    {% endfor %}
                </p>
            
                <p> 
                    {{ form.submit() }}
                </p>
            
        </fieldset>
        </form>
    </div>
    {% endblock %}


```
