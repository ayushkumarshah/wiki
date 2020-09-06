
# Create a form using POST method

```html
<form action="{{url_for('enrollment')}}" method="POST">
<input type="hidden" name="courseID" value="{{data['courseID']}}">
<input type="hidden" name="title" value="{{data['title']}}">
<input type="hidden" name="term" value="{{data['term']}}">
<button>Enroll</button>
</form>
```

Display these data in another page (say enrollment.html)

```html
<p>Course ID: {{ data.id }}</p>
<p>Course Title: {{ data.title }}</p>
<p>Course Term: {{ data.term }}</p>
```

## Add route for enrollment

```python
@app.route("/enrollment", methods=["GET", "POST"])
def enrollment():
    id = request.form.get("courseID")
    title = request.form.get("title")
    term = request.form.get("term")
    return render_template(
        "enrollment.html", register=True, data={"id": id, "term": term, "title": title},
    )
```

> If methods not specified, request.args.get will result in error since POST method is required. 
