# Jupyter notebook / Colab Tricks

## View external python file code in notebook

```python
!pygmentize python_file.py
```

Example:
```python
!pygmentize train/model.py
```

## Autoreload modules before execution

While loading the modules, load the “autoreload” extension so that you can change
code in the modules and the changes get updated automatically. For more info, 
see [autoreload documentation](https://ipython.org/ipython-doc/3/config/extensions/autoreload.html)

```python
%load_ext autoreload
%autoreload 2
from foo import some_function
some_function()
>>> 42
```

```python
# open foo.py in an editor and change some_function to return 43
some_function()
>>> 20
```

## Time magic functions

### Line mode
```python
%timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] statement
```

Options: 

`-n<N>:` execute the given statement `<N>` times in a loop. If `<N>` is not provided, `<N>` is determined so as to get sufficient accuracy.

`-r<R>:` number of repeats `<R>,` each consisting of `<N>` loops, and take the best result. Default: 7

`-t:` use time.time to measure the time, which is the default on Unix. This function measures wall time.

`-c:` use time.clock to measure the time, which is the default on Windows and measures wall time. On Unix, resource.getrusage is used instead and returns the CPU user time.

`-p<P>:` use a precision of `<P>` digits to display the timing result. Default: 3

`-q:` Quiet, do not print result.

`-o:` return a TimeitResult that can be stored in a variable to inspect

Example:

```
%timeit function_name(args)
```

### Cell mode
```python
%%timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] setup_code code code…
```

Example

```python
%%timeit
for i, j in enumerate(range(1, 10, 2)):
    print(i, j)
```

## To create and write directly to python file

```python
%%writefile python_file.py
import numpy as np
print(np.ones(2,3))
```

## Running an external python file as a program

```python
%run [-n -i -e -G]
     [( -t [-N<N>] | -d [-b<N>] | -p [profile options] )]
     ( -m mod | file ) [args] 
```

Options:

`-n` : Don't run __main__. Useful when you want to reload the function
definitions without calling the code.


Example:
```python
%run -n python_file.py
```
## Debugger

Activate the interactive debugger.

```python
%debug [--breakpoint FILE:LINE] [statement [statement ...]]
```

## Widgets

### Dropdown widget

Create the widget

```python
%%writefile widget.py
import ipywidgets as widgets
score = widgets.Dropdown(
        value= None,
        options=['Satisfactory', 'Not Satisfactory', 'Need to use another Metric',None],
        description='Ans:',
    )
display(score);
```

Run the widget

```python
%run widget.py
print(score.value)
```

## Displaying images

```markdown
<center>
<figure>
<img src="https://drive.google.com/uc?id=1wsw2sDf5WcnuCuu-b0RZfi4rrK30FB8R" alt="Image name" >
<figcaption align="center">Figure 1: Caption </figcaption>
</figure>
</center>
```

---

## Working with videos

### Downloading videos from google drive

```python
!wget --no-check-certificate -q -O 'video_file.webm' 'https://docs.google.com/uc?export=download&id=1B8QVEefZu6mvOWUMxGXgWTWmLxsMXeDH'
!wget --no-check-certificate -q -O 'video_file.mp4' 'https://docs.google.com/uc?export=download&id=1B8QVEefZu6mvOWUMxGXgWTWmLxsMXeDH'
```

### Displaying videos

```python
from IPython.core.display import Video
Video('video_file.webm', height=360, width=512, 
        embed=True, mimetype='video/webm')
Video('video_file.mp4', height=360, width=512, 
        embed=True)
```

### Using Video Writers (OpenCV)


```python
# To create video that can be displayed in browser (notebook)
fourcc = cv2.VideoWriter_fourcc('V','P','8','0')
output= cv2.VideoWriter('output.webm', fourcc, 20, (width, height))

# To create video that supported in local (mac / linux)
fourcc = cv2.VideoWriter_fourcc('X','V','I','D')
output= cv2.VideoWriter('output.mkv or mp4', fourcc, 20, (width, height))

# To create video that supported in local (windows)
fourcc = cv2.VideoWriter_fourcc('D','I','V','X')
output= cv2.VideoWriter('output.mkv or mp4', fourcc, 20, (width, height))

while True:
    ret, frame = video_cap.read()
    if not ret:
      break
      
    output.write(frame)
output.release()

Video('output.webm', height=360, width=512, embed=True, mimetype='video/webm')
```

---

