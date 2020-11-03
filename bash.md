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
|`command > file.txt`|adds output of command to file.txt. Creates a new file if does not exist. If exists, overwrites the contents of the file.|
|`command >> file.txt`|adds output of command to file.txt. Creates a new file if does not exist. If exists, appends the outputs to the contents of the file.|
|`awk`|very powerful command for pattern scanning and processing|

test command and [[]] are equivalent

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
# The above line is called chebang / shebang

# $USER -> "user_name"
# $HOME -> "/Users/user_name"

DESKTOP_PATH="/Users/$USER/Desktop/"
DESKTOP_PATH_="$HOME/Desktop/"

# Use backticks to assign command outputs to a variable directly. E.g. below
DATE=`date +%d_%m_%Y`

# Alternative is to use $()
# DATE=$(date +%d_%m_%Y)

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

## Simple shell script with arguments to create another script

```zsh
#!/bin/bash

# Arguments defined as $1 $2 $3 and so on. But ${10} when 2 digits
FILENAME=$1.sh

# Check if file exists: 2 ways
# if test -e $FILENAME OR
while [[ -e $FILENAME ]] 
do
  echo -n "file already exists, are you sure you would like to overwrite? (y/n)"
  read ANSWER
  case $ANSWER in
    y|Y|[yY][eE][sS])
      break
      ;;
    n|N|[nN][oO])
      read -p "enter the new filename" FILENAME
      FILENAME=$FILENAME.sh
      ;;
  esac
done
echo "#!/bin/bash" > $FILENAME
chmod +x $FILENAME
vim $FILENAME
```

## Simple shell script to search files and copy it to a directory

```zsh
#!/bin/bash

SEARCH_DIR=$HOME/Downloads

FOUND_DIR=$HOME/Desktop/codes/found
mkdir -p $FOUND_DIR

# Search according to modified time less than 1 day ago
find $SEARCH_DIR -mtime -1 -type f -iname "*.txt" | xargs -I % cp % $FOUND_DIR
# -1 means 1 day ago
# f means search limited to only files

# xargs used to pass output of 1st command as argument to 2nd command.
# -I is used to create a placeholder for the argument. 
# % is the placeholder. It can be symbols other than % as well.
```

## Simple shell script to extract components causing error in a log file

Example of error

```md
Aug 19 20:24:03 ip-172-31-190-196 amazon-ssm-agent.amazon-ssm-agent[2142]: 2020-08-19 20:24:03 ERROR Health ping failed with error - EC2RoleRequestError: no EC2 instance role found
```

```zsh
#!/bin/bash

LOGFILE=samplelog

# Capturing each line of output from grep in variable named line
while read -r line
do
  # To extract component, we use awk
  component=$(awk {'print $5'} | cut -d : -f 1)
  # Works as same component=`awk {'print $5'} | cut -d : -f 1`
  # -d means delimiter used to cut which is :
  # -f 1 means choose field number 1 from the cut results
  echo -e "$component \n">> comp_errors
  # -e tells to interpret \n as new line
# -i  means case insensitive
done < <(grep -i error $LOGFILE)
# 1st < means input to the while loop
# 2nd < means process substitution i.e. executes the command inside brackets,
# saves the output to a temporary file and then deletes it
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
