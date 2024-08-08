# Conda Basics

## Create conda environment

```console
$ conda create -n env_name python==x.x
```

## List conda environments

```console
$ conda env list
```

## Create environment yml

```console
$ conda env export --no-builds > environment.yml
```

## Or Create requirements.txt (earlier one preferred)

```console
$ pip list --format=freeze > requirements.txt
```

OR

```console
$ pip freeze > requirements.txt
```

## Create conda environment from yml file

```console
$ conda env create -f environment.yml
```

## Update packages from yml file

```zsh
$ conda env update --file environment.yml
```

## List installed packages

```console
$ conda list

# or

$ pip freeze
```
