# Jupyter notebook / Colab Tricks

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
