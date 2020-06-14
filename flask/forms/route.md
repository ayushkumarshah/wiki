# Update login route

```python
@app.route("/login", methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        # form data
        email = form.email.data
        password = form.password.data

        # comapre form email with email in database
        user = User.objects(email=email).first()
        
        if user and user.get_password(password):
        # if request.form.get("email") == "test@uta.com":
            flash("{}, You are successfully logged in".format(user.first_name), "success")
            return redirect("/index")
        else:
            flash("Sorry, something went wrong", "danger")

    return render_template("login.html", title="Login", form=form, login=True)
```

Check by using email and password from mongo db

# Update register route

```python

@app.route("/register", methods=['GET', 'POST'])
def register():
    form = RegisterForm()
    if form.validate_on_submit():
        user_id = 20 + User.objects.count()
        user_id += 1

        email = form.email.data
        password = form.password.data
        first_name = form.first_name.data
        last_name = form.last_name.data

        user = User(user_id=user_id, email=email, first_name=first_name, last_name=last_name)
        user.set_password(password)
        user.save()

        flash("You have registered successfully", "success")
        return redirect(url_for('index'))
    return render_template("register.html", title="Register", form=form, register=True)

```

# Update course route 

```python
@app.route("/courses/")
@app.route("/courses/<term>")
def courses(term=None):
    if term is None:
        term = 2019
    classes = Course.objects.order_by("-courseID")  # - for descending order
    return render_template(
        "courses.html", courseData=classes, courses=True, term=term
    )
```
