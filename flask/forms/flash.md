
# Flashing messages

## Update route

```python
from flask import redirect, flash
@app.route("/login", methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        if request.form.get("email") == "test@uta.com":

            flash("You are successfully logged in", "success")
            return redirect("/index")
        else:
            flash("Sorry, something went wrong", "danger")

    return render_template("login.html", title="Login", form=form, login=True)
```
## Update template

```html

  {% include "includes/nav.html" %}
  {% with messages = get_flashed_messages(with_categories=true) %}
    {% if messages %}
      {% for category, message in messages %}
      <div class="alert alert-{{category}}">
        <p>{{ message }}</p>
        </div>
      {% endfor %}
    {% endif %}
  {% endwith %}

  {% block content %}
  {% endblock %}
{% include "includes/footer.html" %}
```
