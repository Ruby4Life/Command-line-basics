mv syntax:
```shell
$ mv [OPTION]... [-T] SOURCE DEST
```
<br>
```shell
$ mv [OPTION]... SOURCE... DIRECTORY
```
<br>
```shell
$ mv [OPTION]... -t DIRECTORY SOURCE...
```
-----------------------
Options:
Simply ask the terminal:
```shell
$ cp --help
```
For the all the options available as well as more info.
<br>
If you specify more than one of the obove options -i, -f, or -n, only the final option specified takes effect.
-----------------------
Backup Methods:
The default ("simple") suffix for backup files is '~', but it can be set differently with the --suffix option or the SIMPLE_BACKUP_SUFFIX environment variable.
The version control method may be selected via the --backup option or through the VERSION_CONTROL environment variable. The possible control methods are:

none, off	Never make backups, even if the --backup option is given.
numbered, t	Make numbered backups.
existing, nil	numbered if numbered backups already exist, simple otherwise.
simple, never	Always make simple backups.
-----------------------
mv examples:

```shell
$ mv myfile.txt destination-directory
```
Moves the file myfile.txt to the directory destination-directory.

```shell
$ mv myfile.txt ../
```
Attempts to move the file myfile.txt into the parent directory.

```shell
$ mv computer\ hope.txt computer\ hope\ 2.txt
```
Renames the file "computer hope.txt" to "computer hope 2.txt". Here, the filenames contain spaces, so the spaces are escaped with a backslash, which protects the words in the filename from being interpreted as separate command arguments.

<ul>
	<li>Tip: If you want to rename a set of files using a regular expression (such as changing filename*.txt to othername*.txt), try the rename command.</li>
</ul>

Related commands:
cp — Copy files and directories.
ln — Create a link, or a symbolic link, to a file or directory.
rename — Renames multiple files using a regular expression.
rm — Remove a directory.