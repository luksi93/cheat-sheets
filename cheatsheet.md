# cheat-sheets

- [ExifTool](#ExifTool)
- [Git](#Git)
- [iTerm](#iTerm)
- [Shell scripting](#Shell-scripting)

## ExifTool

### Renaming picture files based on creation date

The first command only displays a preview of how the files will be renamed. The second one actually renames the files.
The files will be renamed to `IMG-YYYYMMDD-HHMMSS-CC.EXT` with CC being an incrementing counter and EXT the original file extension.

```
exiftool -fileOrder createdate -d IMG-%Y%m%d-%H%M%S%%-2.c.%%le "-testname<CreateDate" path/to/folder_or_file
exiftool -fileOrder createdate -d IMG-%Y%m%d-%H%M%S%%-2.c.%%le "-filename<CreateDate" path/to/folder_or_file
```

## Git

### Show the git config (global and local if in a repo). It also shows from where each property comes.

```git config --list --show-origin```

### Useful commands for investigating project history

```git shortlog -e -n -s [path]``` prints the list of contributors in the specified [path] ordered by number of contributions.

```git effort --above [number]``` will print the files affected for a number of commits greater than [number] ([Part of git-extras](https://github.com/tj/git-extras)).

```git blame [file]``` will output the [file] content alongside with author for a particular line, and commit hash for the same line.

```git grep [regexp]``` will print the lines in all the tracked files where the regexp is present.

```git log -G [regexp]``` will output the commits where [regexp] is present on the diff associated to the commit.

```git log --follow -- filename``` will output the history of a particular file.

```git log [--since=date] [--until=date]``` Well, this is self-explanatory.

## iTerm

### Shortcuts

| Description                                    | Shortcut                           |
| ---------------------------------------------- | ---------------------------------- |
| Close current pane                             | `⌘ Cmd` + `w`                      |
| Close current window with all panes            | `⌘ Cmd` + `⇧ Shift` + `w`          |
| Split pane                                     | `⌘ Cmd` + `d`                      |
| Split pane horizontally                        | `⌘ Cmd` + `⇧ Shift` + `d`          |
| Resize pane                                    | `⌘ Cmd` + `⌃ Ctrl` + `arrow key`   |
| Switch pane                                    | `⌘ Cmd` + `⌥ Option` + `arrow key` |

## Shell scripting

### Ask for confirmation

```
read -p REPLY -n 1 -r
if [[ $REPLY =~ ^[Yy]$ ]] then ... fi
```

### Always return the absolute path to the directory the script is located

```
echo $(cd `dirname $0` && pwd)
```
Note that although the change directory command (cd) is used, the script will not change directory and any other calls within it are still relative to the current working directory.

### Shell script control flow 

This part is 'forked' from [ffraenz/cheatsheet](https://github.com/ffraenz/cheatsheet)

| Description                                    | Structure                          |
| ---------------------------------------------- | ---------------------------------- |
| String `$a` equals `$b`                        | `if [ $a = $b ]; then ... fi`      |
| String `$a` does not equal `$b`                | `if [ $a != $b ]; then ... fi`     |
| `$string` is empty `-z` / not empty `-n`       | `if [ -z $string ]; then ... fi`   |
| `$path` exists                                 | `if [ -e $path ]; then ... fi`     |
| `$path` is a file `-f` / directory `-d`        | `if [ -f $path ]; then ... fi`     |
| `$path` is readable `-r` / `-w` / `-x` by user | `if [ -r $path ]; then ... fi`     |
| `$a` is newer `-nt` / older `-ot` than `$b`    | `if [ $a -nt $b ]; then ... fi`    |
| For loop over values                           | `for i in 1 2 3 4 5; do ... done`  |
| For loop over files                            | `for PATH in /foo/*; do ... done`  |
| For loop over directories                      | `for PATH in /foo/*/; do ... done` |
| While loop                                     | `while [ condition ]; do ... done` |


