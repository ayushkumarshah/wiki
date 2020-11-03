# Bash Shell Scripting

## Commands

|Commands|Description|
|--|--|
|`echo $SHELL`||
|`man command-name`||
|`alias alias-name`|Shows the alias actual command|
|`date +format` E.g. `date +%d/%m/%Y`|Shows the alias actual command|
|`ls -al`|List. a - all <br> l - long listing format <br> d means directory - means file|
|`less file.txt`|Show file contents (similar to cat but allows to move up and down)|
|`more file.txt`|Show file contents (similar to cat but allows to move up and down)|
|`rm -ir`|Remove. i - prompt to ask permission for each file. r - recursively delete|
|`find / -name "file_name" [2>/dev/null]` <br> Eg: `find \ -name "*backup*" 2/dev/null`| Find file from the root directory <br> 2/dev/null: 2 takes error output and redirects to dev/null where it is deleted|
|`grep text_to_search /path/to/file`|Search for contents in a file|
|`command | grep text_to_search` <br> Eg: `find / -name "*backup*" 2>/dev/null | grep $USER`|Using pipe to combine grep with other commands|

## Permissions

### 3 user permissions

- You (u)
- Your group (g)
- Others (o)

### 3 permission types

- Read (r)
- Write (w)
- Execute (x)

### Changing permissions

Adding permissions read, write and execute for you (user)

```zsh
chmod u=rwx script_name
```

Adding permissions read and execute for group and others

```zsh
chmod go=rx script_name
```

Removing and adding permissions

```zsh
# Removing read permission for user: others
chmod o-r script_name
# Adding read permission for user: others
chmod o+r script_name
```

## Writing simple shell script to create a backup and mail it

```zsh
#!/bin/bash

# $USER -> "user_name"
# $HOME -> "/Users/user_name"

DESKTOP_PATH="/Users/$USER/Desktop/"
DESKTOP_PATH_="$HOME/Desktop/"

# Use backticks to assign command outputs to a variable directly. E.g. below
DATE=`date +%d_%m_%Y`

BACKUP_PATH="$DESKTOP_PATH/codes/"
BACKUP="backup_"
EXT=".tar"

# Use $ to reference defined variables
FILE_NAME=$DESKTOP_PATH$BACKUP$DATE$EXT

echo $FILE_NAME

tar cvfz $FILE_NAME $BACKUP_PATH
# tar - tape archive, also does not require - like other commands since old
# c - create
# f - archive on file instead of tape
# z - zip. Don't use if you use gzip
# v - verbose

# gzip $FILE_NAME

# Mail the created backup file
# Check if backup file exists
if test -f "$FILE_NAME"; then
  echo "Here is you daily backup" | mail -A $FILE_NAME -s "Today's Backup"
  ayush.kumar.shah@gmail.com
else
  echo $DATE " There was a problem creating the backup file." >> $HOME/error.log
fi

```

## Cron Tab

### List crontabs

```zsh
crontab -l
```

### Create crontabs

```zsh
crontab -e
```

### Remove all crontabs

```zsh
crontab -r
```

### Crontab shortcuts

```zsh
@yearly /path/to/job
@annually /path/to/job
@monthly /path/to/job
@weekly /path/to/job
@midnight /path/to/job
@hourly /path/to/job
# Run when computer boots
@reboot /path/to/job
```
