# Bash Shell Scripting

## Some common commands

|Commands|Description|
|--|--|
|`echo $SHELL`|Display name of active shell (bash or zsh or others)|
|`man command-name` <br> Eg: man bash &#124; grep -C2 '$@'|Get information about the command <br> Here, return 2 leading and trailing lines around the matching text '$@' in the information|
|`command-name --help`|Information about the command usage|
|`pwd`| get current path
|pwd &#124; pbcopy | copy current path to clipboard (Use xcopy or xsel for linux)
|`cd -`  | go back to previous location|
|`ls -al`|List. a - all <br> l - long listing format <br> d means directory - means file|
|`ls -ls`| list files with detailed info (permission, date, symoblic links)|
|ls -1 &#124; wc -l | count number of files in a directory|
|`cat filename`| show the contents of the file filename|
|tee <br> Eg: df -h &#124; tee usage.txt | display stdout of a command and write it in a file|
|`free -h`                 |Show RAM - space used and free           |
|`df -h`                    |Show disk information - space used and free           |
|`du -sh .`                 |Show total size occupied by current directory           |
|`du -sh *`                 |Show size of each file or folder in current directory           |
|du -sh * &#124; tail -1  |Show total size occupied by the last file in the current directory|
|ps ax[c] [&#124; less]|List currently running programs. <br>c - easier to read<br>less - easier to navigate|
|`pidof process-name`|Get the process id of a running process.|
|`kill process-id`|Kill the process|
|`uname [-[s][a]]`|Display name of OS Distribution. a - Detailed info.|
|`stat filename`            |Display file status         |
|`alias alias-name`|Shows the alias actual command|
|`date +format` E.g. `date +%d/%m/%Y`|Date command|
|`cal [-3] [[month] year]` <br> E.g. `cal -3 june 1996` or `cal 1997` or `cal`|Calendar command. -3 means show previous and the next month as well.|
|`less file.txt`|Show file contents (similar to cat but allows to move up and down)|
|`more file.txt`|Show file contents (similar to cat but allows to move up and down)|
|`rm -ir`|Remove. i - prompt to ask permission for each file. r - recursively delete|
|`grep [-i] text_to_search /path/to/file`|Search for contents in a file , i - case insensitive|
|`grep -v text_to_search /path/to/file`|Search for contents not matching the pattern in a file|
|`command > file.txt`|adds output of command to file.txt. Creates a new file if does not exist. If exists, overwrites the contents of the file.|
|`command >> file.txt`|adds output of command to file.txt. Creates a new file if does not exist. If exists, appends the outputs to the contents of the file.|
|`find / -name "file_name" [2>/dev/null]` <br> Eg: `find \ -name "*backup*" 2/dev/null`| Find file from the root directory <br> 2/dev/null: 2 takes error output and redirects to dev/null where it is deleted|
|`find . -not -name "file_name"`|Find files not matching the filename|
|find . -name "file_name" &#124; xargs -I % rm %|Find and delete files matching the filename|
|`find . -name "file_name" -exec rm -i {} \;`|Find and delete files matching the filename|
|`find . -name "file_name" -exec grep "Hello" -i {} \;`|Find and search "Hello" in files matching the filename|
|`find -E . -regex ".*/file_name[0-9].sh"`|Find files matching the regular expression (this syntax works only in osx)|
|`find -E . -not -regex ".*/file_name[0-9].sh"`|Find files not matching the regular expression (this syntax works only in osx)|
|command &#124; grep text_to_search <br> Eg: find / -name "*backup*" 2>/dev/null &#124; grep $USER|Using pipe to combine grep with other commands|
|`awk`|very powerful command for pattern scanning and processing|
|`<C-T>`|fzf: fuzzy finding files or directories <br> You need to install fzf|
|`<C-R>`|fzf: fuzzy finding commands in history|
|`<Esc-C>`|fzf: fuzzy finding files or directories from current path|
|`top` or `htop` or `ytop` or `gotop`             |Process info and CPU Usage  (You need to install htop or ytop)|
|`tree [-aldf][-L level][-P pattern][-I pattern][-o filename] `|display directory's contents in a  tree <br> a - all files <br> l - symbolic links <br> d - directories only <br> L - limit number of levels of directory <br> I - files not matching pattern <br> P - files matching pattern <br> o - output to filename <br> You need to install tree|

## Some quick tips:

- `test some-condition` command and `[[some-condition]]` are equivalent
- OUT=`command` and OUT=$(command) are equivalent and used to store output of
    the command to a variable
- You can use `command` or $(command) in a bash shell and press tab to replace
    the command by its output and use it. Example: 
  ```zsh
  mv `pwd` /destination-path/
  mv $(pwd) /destination-path/
  ```

## Extracting Substrings

```zsh
#!/bin/bash
var="apple orange"

# Print apple
echo "${var%% *}"  # Fastest: about 0.001 sec
echo $var | cut -d' ' -f1  # Faster than awk, slower than above
echo $var | awk '{print $1}'  # Slowest : about 0.16 sec

# Print orange
echo "${var##* }"  # Fastest: about 0.001 sec
echo $var | cut -d' ' -f2  # Faster than awk, slower than above
echo $var | awk '{print $2}'  # Slowest : about 0.16 sec

# Working:
# #-deletes from beginning
echo "${var#app}"  # Removes substring 'app' from the beginning
echo "${var#orange}"  # Removes nothing
echo "${var#*or}"  # Removes substring 'apple or' from the beginning
echo "${var#*}"  # Removes nothing - # means conservative so as less as possible.
echo "${var##*}"  # Removes everything - ## means greedy - as much as possible
echo "${var##p}"  # Removes substring 'app' from the beginning
echo "${var#p}"  # Removes substring 'ap' from the beginning

# %-deletes from the end
echo "${var%app}"  # Removes nothing
echo "${var%e}"  # Removes e from end
echo "${var%nge}"  # Removes substring 'nge' from the end
echo "${var%n*}"  # Removes substring 'nge' from the end
echo "${var%p*}"  # Removes substring 'ple orange' from the end
echo "${var%%p*}"  # Removes substring 'pple orange' from the end

```

## Running bash script in debug mode

### Method 1

```zsh
bash -x script_name
```

### Method 2

Modify the script

```bash
#!bin/bash -x
...
...
exit 0
```

### Method 3

If only certain portions to be debugged

```bash
#!bin/bash
set -x
...
code to be debugged
...
set +x
...
code not to be debugged
...
exit 0
```

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

