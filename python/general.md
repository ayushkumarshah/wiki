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
