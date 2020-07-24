# Matplotlib tips and tricks

## Figure size globally

```python
plt.rcParams['figure.figsize'] = (12, 12)
```

## Remove white space around figure while saving 

```python
plt.savefig(filename, transparent = True, 
            bbox_inches = 'tight', 
            pad_inches = 0)
```


