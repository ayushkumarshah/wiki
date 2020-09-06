
1. Organize files

- create app directory (package)
  app
  |__ __init__.py
  |__ static
      |__ template
      |__ images

- Copy all code from main.py to __init__.py
- In main.py, from app import app

2. Create config.py in main directory:

```python
import os

class Config(object):
    SECRET_KEY = os.environ.get('SECRET_KEY') or "secret_string"                
    # For security prupose, to prevent hacking, when creating forms or setting cookies
```

3. Create route.py in app directory
