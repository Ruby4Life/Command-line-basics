wc syntax:

```shell
$ wc [OPTION]... [FILE]...
```

```shell
$ wc [OPTION]... --files0-from=F
```

Options:
-c, --bytes	print the byte counts.
-m, --chars	print the character counts.
-l, --lines	print the newline counts.
--files0-from=F	read input from the files specified by NUL-terminated names in file F; If F is "-" then read names from standard input.
-L, --max-line-length	print the length of the longest line.
-w, --words	print the word counts.
--help	display a help message, and exit.
--version	output version information, and exit.

---------------------------

wc examples:

```shell
$ wc myfile.txt
```

Displays information about the file myfile.txt. Output will resemble the following:
```shell
$ 5 13 57 myfile.txt
```

Where 5 is the number of lines, 13 is the number of words, and 57 is the number of characters.

```shell
$ ls -1 | wc -l
```

This command returns the number of objects in the current directory. It uses the ls command to produce a single-column (-1) listing of the directory contents, which outputs one line per object; this output is piped to wc, which counts the lines (-l), and returns that number.
Related commands

cksum — Calculate and display a CRC for files.
nl — Number the lines in a file.