# General python tricks

## 1. System arguments (simple)

### Code

`python_code.py`

```python
import sys
if __name__ == '__main__':
    if len(sys.argv) < 2:
        print("Usage: python3 python_code.py <arg1> <arg2>")
        raise ValueError("Incorrect usage")
        exit(0)
    arg1 = sys.argv[1]
    print (arg1)
    arg2 = sys.argv[2]
    print(arg2)
```

### Running the code

```console
$ python python_code.py arg1 arg2
```

## Generating requirements.txt correctly

I found this more appropriate.

```zsh
pip list --format=freeze > requirements.txt
```

However, this can be done as well. Faced a few issues in this approach.

```zsh
pip list --format=freeze > requirements.txt
```

## Current Datetime

```python
from datetime import datetime
now = datetime.now().isoformat(timespec='seconds')
print(now)
# 2014-07-05T14:34:14
now = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
print(now)
# 2014-07-05 14:34:14
```
