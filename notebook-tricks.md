# Jupyter notebook / Colab Tricks

## Working with videos

### Downloading videos from google drive

```python
!wget --no-check-certificate -q -O 'airpaint.webm' 'https://docs.google.com/uc?export=download&id=1B8QVEefZu6mvOWUMxGXgWTWmLxsMXeDH'
!wget --no-check-certificate -q -O 'airpaint.mp4' 'https://docs.google.com/uc?export=download&id=1B8QVEefZu6mvOWUMxGXgWTWmLxsMXeDH'
```

### Displaying videos

```python
from IPython.display import Video
Video('airpaint.webm', height=360, width=512, 
        embed=True, mimetype='video/webm')
Video('airpaint.mp4', height=360, width=512, 
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


## To view code of .py file in notebook

```python
!pygmentize train/model.py
```

## To create and write directly to python file

```python
%%writefile ex9q1.py
import ipywidgets as widgets

ex9q1 = widgets.Dropdown(
        value= None,
        options=['Satisfactory', 'Not Satisfactory', 'Need to use another Metric',None],
        description='Ans:',
    )
display(ex9q1);
```

## Run dropdown widgets

```python
%run ex9q1.py
### BEGIN HIDDEN TESTS
assert(ex9q1.value == "Satisfactory")
### END HIDDEN TESTS
```
