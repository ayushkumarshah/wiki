# Create a form using GET method

```html
<form action="{{url_for('enrollment')}}" method="GET">
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
@app.route("/enrollment")
def enrollment():
    id = request.args.get("courseID")
    title = request.args.get("title")
    term = request.args.get("term")
    return render_template(
        "enrollment.html", register=True, data={"id": id, "term": term, "title": title},
    )

```


