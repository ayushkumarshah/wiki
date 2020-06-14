
# Form validation

```html
  <form name="login" action="" method="post" novalidate>
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
```

> Add style for error message in `main.css`

```css
...
.error-message{
  color: red;
}
```
