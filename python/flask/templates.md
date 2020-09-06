- Create index.html in templates
- Use css and images in static folder
- Create includes folder inside templates foder and define extra html to be usable by index.html
- Add Navigation links
- Replace navigation links by route functions using 
  ```html
  <a href = "{{url_for('index')}}"
  ```
- Create base template and extend in another template using:

  ```html
  {% extend 'layout.html' %}

  and

  {% block content %}
  {% endblock %}
  ```
  To reder same content twice (duplicate) :
  ```html
  {{self.content()}}
  ```
# Passing data

Add arguments in route
```python
courseData = [{"id": "11", "name": "Ayush"}, {"id": "12", "name": "Kamlesh"}]
return render_template("course.html", courseData=courseData)
``````

In course.html, use for loop

```
<div>
    <table class="table table-hover">
        <thead>
        <tr>
            <th scope="col">Course ID</th>
            <th scope="col">Title</th>
            <th scope="col">Description</th>
            <th scope="col">Credits</th>
            <th scope="col">Term</th>
            <th scope="col">Enroll</th>
        </tr>
        </thead>
        <tbody>

        <!-- Construct the rest of courses here -->
        
        {% for data in courseData %}
        <tr>
          <td scope='row'>{{data["courseID"]}}</td>
            <td>{{data["title"]}}</td>
            <td>{{data["description"]}}</td>
            <td>{{data["credits"]}}</td>
            <td>{{data["term"]}}</td>
            <td>
                <button>Enroll</button>
            </td>
        </tr>
        {% endfor %}
        </tbody>
    </table>
</div>
```
