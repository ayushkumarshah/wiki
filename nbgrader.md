# Setting up nbgrader exchange for release and collect

## 1. Creating directories for exchange setting:

```console
$ mkdir /tmp/exchange
$ mkdir -p /tmp/exchange/ai_course_id/outbound
$ mkdir -p /tmp/exchange/ai_course_id/inbound
$ chmod ugo+rw /tmp/exchange
```

## 2. Create file nbgrader_config.py file at the directory containing source and release folders.

Add the following lines in `nbgrader_config.py`

```python
c = get_config()
c.Exchange.course_id = "ai_course_id"
c.Exchange.root = "/tmp/exchange"
c.ExecutePreprocessor.timeout = -1
```

## 3. Nbgrader package fix:

### i. Make changes to nbgrader package codes:

- Open the files `assignment_list/handlers.py` and `validate_assignment/handlers.py` 
located in the nbgrader package: 

  - If the package is installed inside a conda environment, the location  is similar to this:
  `/Users/username/miniconda3/envs/env_name/lib/python3.x/site-packages/nbgrader/server_extensions/`

  - If the package is installed inside a conda base environment, the location might is similar to this:
  `/Users/username/miniconda3/lib/python3.x/site-packages/nbgrader/server_extensions/`

  - If the package is installed inside the main python, the location is similar to this
  `/Users/username/.local/lib/python3.7/site-packages/nbgrader/server_extensions/`

Modify according to the changes here: [Changes](https://github.com/jupyter/nbgrader/pull/1239/commits/0ee032fdf40354a264855e80722a164eb0309770)

#### `assignment_list/handlers.py`

```python
# for config in NbGrader._load_config_files("nbgrader_config", path=paths, log=self.log):
for config, filename in NbGrader._load_config_files("nbgrader_config", path=paths, log=self.log):

...
...

# for new_config in NbGrader._load_config_files("nbgrader_config", path=[os.getcwd()], log=self.log):
for new_config, filename in NbGrader._load_config_files("nbgrader_config", path=[os.getcwd()], log=self.log):
```

#### `validate_assignment/handlers.py`


```python
# for config in NbGrader._load_config_files("nbgrader_config", path=paths, log=self.log):
for config, filename in NbGrader._load_config_files("nbgrader_config", path=paths, log=self.log):
```


### ii. Downgrade sqlalchemy to version 1.2.18

```console
$ pip install sqlalchemy==1.2.18
```

### iii. Restart the terminal and you are good to go.

