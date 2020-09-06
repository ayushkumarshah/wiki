## Accessing Query String (GET)

```python
request.args.get(<field_name>)
request.args[<field_name>]
```

## Accessing Form Data (POST)

```python
request.form.get(<field_name>)
request.form[<field_name>]
```

## Respnse object

```python
class flask.Respnse(
    response=None,
    status=None,
    headers=None,
    mimetype=None,
    content_type=None
    direct_passthrough=False
)
```

## URL Variables

```python
@app.route("/courses/")
@app.route("/courses/<term>")
def courses(term="2019"):
  ....
  return render_template("course.html", courseData=courseData, term=term)

```

Access term in html using `{{ term }}`
