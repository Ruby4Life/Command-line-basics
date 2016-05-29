<h3>grep syntax:</h3>
grep 'word' filename
grep 'word' file1 file2 file3
grep 'string1 string2'  filename
cat otherfile | grep 'something'
command | grep 'something'
command option1 | grep 'data'
grep --color 'data' fileName
---------------------------

Search /etc/passwd file for boo user, enter:
```shell
$ grep boo /etc/passwd
```
Sample outputs:
```shell
foo:x:1000:1000:foo,,,:/home/foo:/bin/ksh
```

---------------------------


You can force grep to ignore word case i.e match boo, Boo, BOO and all other combination with the -i option:
```shell
$ grep -i "boo" /etc/passwd
```

---------------------------


Use grep recursively

You can search recursively i.e. read all files under each directory for a string “192.168.1.5”
```shell
$ grep -r "192.168.1.5" /etc/
```
OR
```shell
$ grep -R "192.168.1.5" /etc/
```

Sample outputs:
```shell
/etc/ppp/options:$ ms-wins 192.168.1.50
/etc/ppp/options:$ ms-wins 192.168.1.51
/etc/NetworkManager/system-connections/Wired connection 1:addresses1=192.168.1.5;24;192.168.1.2;
```

You will see result for 192.168.1.5 on a separate line preceded by the name of the file (such as /etc/ppp/options) in which it was found. The inclusion of the file names in the output data can be suppressed by using the -h option as follows:
```shell
$ grep -h -R "192.168.1.5" /etc/
```

OR

```shell
$ grep -hR "192.168.1.5" /etc/
```

Sample outputs:
```shell
$ ms-wins 192.168.1.50
$ ms-wins 192.168.1.51
addresses1=192.168.1.5;24;192.168.1.2;
```

---------------------------


Use grep to search words only

When you search for boo, grep will match fooboo, boo123, barfoo35 and more. You can force the grep command to select only those lines containing matches that form whole words i.e. match only boo word:
```shell
$ grep -w "boo" file
```
Use grep to search 2 different words


Use the egrep command as follows:
```shell
$ egrep -w 'word1|word2' /path/to/file
Count line when words has been matched
```

grep can report the number of times that the pattern has been matched for each file using -c (count) option:
```shell
$ grep -c 'word' /path/to/file
```

---------------------------


Pass the -n option to precede each line of output with the number of the line in the text file from which it was obtained:
```shell
$ grep -n 'root' /etc/passwd
```

Sample outputs:
```shell
1:root:x:0:0:root:/root:/bin/bash
1042:rootdoor:x:0:0:rootdoor:/home/rootdoor:/bin/csh
3319:initrootapp:x:0:0:initrootapp:/home/initroot:/bin/ksh
```

---------------------------


Grep invert match

You can use -v option to print inverts the match; that is, it matches only those lines that do not contain the given word. For example print all line that do not contain the word bar:
```shell
$ grep -v bar /path/to/file
```

---------------------------



UNIX / Linux pipes and grep command

grep command often used with shell pipes. In this example, show the name of the hard disk devices:
```shell
$ dmesg | egrep '(s|h)d[a-z]'
```

---------------------------


Display cpu model name:
```shell
$ cat /proc/cpuinfo | grep -i 'Model'
```

However, above command can be also used as follows without shell pipe:
```shell
$ grep -i 'Model' /proc/cpuinfo
```

Sample outputs:
```shell
model		: 30
model name	: Intel(R) Core(TM) i7 CPU       Q 820  @ 1.73GHz
model		: 30
model name	: Intel(R) Core(TM) i7 CPU       Q 820  @ 1.73GHz
```

---------------------------


How do I list just the names of matching files?

Use the -l option to list file name whose contents mention main():
```shell
$ grep -l 'main' *.c
```

---------------------------


Finally, you can force grep to display output in colors, enter:
```shell
$ grep --color vivek /etc/passwd
```