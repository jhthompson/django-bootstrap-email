# django-bootstrap-email

## Usage

1. Install

```shell
pip install django-bs-email
```

2. Add to `INSTALLED_APPS`

```python
INSTALLED_APPS = [
    # ...
    "django_bootstrap_email",
]
```

3. Use the bootstrap_email template tag in your Django template

```html
{% load bootstrap_email %}

{% bootstrap_email %}
<body class="bg-light">
  <div class="container">
    <div class="card my-10">
      <div class="card-body">
          <p>
            {{ message }}
          </p>
      </div>
    </div>
  </div>
</body>
{% end_bootstrap_email %}
```

4. Create the email and send it

```python
context = {
    "message": "Hello World!",
}

subject = "Greeting"
# you should always include a plain text version of the HTML email
text_content = render_to_string("path/to/template.txt", context)
html_content = render_to_string("path/to/template.html", context)

email_message = EmailMultiAlternatives(
    subject=subject,
    body=text_content,
    from_email="me@test.com",
    to=["you@test.com"],
)
email_message.attach_alternative(html_content, "text/html")
email_message.send()
```

And a complete HTML email will be output, which should render correctly across email clients:

![Rendered HTML email example](https://raw.githubusercontent.com/jhthompson/django-bootstrap-email/main/example.png)