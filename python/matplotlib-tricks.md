# Matplotlib tips and tricks

## Setting figure size globally

```python
plt.rcParams['figure.figsize'] = (12, 12)
```

## Setting axis off globally

```python
plt.rcParams['xtick.labelsize'] = 0
plt.rcParams['ytick.labelsize'] = 0
plt.rcParams['xtick.bottom'] = False
plt.rcParams['ytick.left'] = False
```

##  Function for displaying images

```python
def imshow(image, title=None, ncols=2, figsize=(12, 15)):
    '''
    Visualize an image or a set of images using subplot

    Parameters
    ----------
    image : numpy.ndarray or list of numpy.ndarray
             Image array or the collection of image arrays to be displayed
    title : str ot list of str, optional, default: None
            The title or collection of titles corresponding to the images
    ncols: int, optional, default: 2
           Number of columns for subplot
    figsize: (float, float), optional, default: (12, 15)
             width, height in inches for single image

    Returns
    -------
    None   
    '''
    
    if not isinstance(image, list):
        plt.figure(figsize=figsize)
        plt.imshow(image)
        if title:
            plt.title(title, fontsize=30)
    else:
        plt.figure(figsize=(50, 75))
        # calculate the number of rows
        nrows = int(np.ceil((len(image)) / ncols))
        for i, img in enumerate(image):
            plt.subplot(nrows, ncols, i+1)
            plt.imshow(img)
            if title:
                plt.title(title[i], fontsize=50)
    plt.show()
```

## Remove white space around figure while saving 

```python
plt.savefig(filename, transparent = True, 
            bbox_inches = 'tight', 
            pad_inches = 0)
```


