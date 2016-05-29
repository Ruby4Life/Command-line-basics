<h3>cp syntax</h3>

	```shell
	$ cp [OPTION]... [-T] SOURCE DEST
	```

    ```shell
    $ cp [OPTION]... SOURCE... DIRECTORY
    ```

    ```shell
    $ cp [OPTION]... -t DIRECTORY SOURCE...
    ```


<h3>cp quick examples</h3>
<h4>To make a copy of a file into the same directory:</h4>
```shell
 $ cp origfile newfile
```
<p>Creates a copy of the file in the working directory named origfile. The copy will be named newfile, and will be located in the working directory.</p>




<p class="tab"><span class="warn">CAREFUL!</span> If the destination file newfile already exists, it will be overwritten without a confirmation prompt. This is the default behavior for all cp operations.</p>
<p>If you want to be prompted before overwriting a file, use the -i (interactive) option. For example:</p>

	```shell
	$ cp -i oldfile newfile
	```


<p>If newfile already exists, you will be prompted:</p>

	```shell
	$ cp: overwrite ‘newfile’
	```


<p>If you type y (or yes, Y, YES, or any other combination of upper and lowercase of these), then newfile will be overwritten with a copy of origfile. Typing anything else will abort the operation.</p>
<h4>Copy a file into another directory:</h4>

	```shell
	$ cp origfile /directory/subdirectory
	```


<p>Creates a copy of the file in the working directory named origfile. The copy will be located in the directory /directory/subdirectory, and will be named origfile.</p>

	```shell
	$ cp origfile /directory/subdirectory/.
	```


<p>Same as the above command. The slash-dot ("/.") is implied in the above form of the command. (The dot is a special file in every Linux directory which means "this directory.")</p>
<h4>Copy a file into another directory, and give it a new name:</h4>

	```shell
	$ cp origfile /directory/subdirectory/newfile
	```


<p>Creates a copy of the file in the working directory named origfile. The copy will be named newfile, and will be located in the directory /directory/subdirectory.</p>
<h4>Copy multiple files into another directory, using a wildcard:</h4>

	```shell
	$ cp file* /directory/subdirectory
	```


<p>Copy every file in the working directory whose name begins with file into the directory /directory/subdirectory. The asterisk ("*") is a wildcard — a special character which expands to match other characters. Specifically, the asterisk wildcard matches zero or more non-whitespace characters. For instance, this command will copy any files named file, file001, file.txt, fileone.jpg, file-archive.zip, etc.</p>


	```shell
	$ cp file*.jpg /directory/subdirectory
	```


<p>Copy every file in the working directory whose name begins with file, and ends with the file extension .jpg. For instance, it would make copies of any files named file, file001.jpg, file002.jpg, or file-new.jpg, etc. The copies will be placed into the directory /directory/subdirectory.</p>
<h4>Copy an entire directory structure into another location:</h4>

	```shell
	$ cp -R /one/two /three/four
	```


<p>Copy the directory two (located in the directory /one), and everything two contains, into the destination directory /three/four. The result will be called /three/four/two. The directory /three must already exist for the command to succeed. If the directory four does not already exist in the directory /three, it will be created.</p>
<h4>General Overview</h4>
<p>Let's say you have a file named picture.jpg in your working directory, and you want to make a copy of it called picture-02.jpg. You would run the command:</p>

	```shell
	$ cp picture.jpg picture-02.jpg
	```


<p>...and the file will be copied. Here, picture.jpg is the source of the copy operation, and picture-02.jpg is the destination. Both files now exist in your working directory.</p>
<p>The source and destination files may also reside in different directories. For instance,</p>

	```shell
	$ cp /home/boris/pictures/picture.jpg /home/boris/backup/picture.jpg
	```


<p>...will make a copy of the file /home/boris/pictures/picture.jpg in the directory /home/boris/backup. The destination file will also be named picture.jpg.</p>

<p>If you are the user boris, you can abbreviate your home directory ("/home/boris") using a tilde ("~"). For instance,</p>

	```shell
	$ cp ~/pictures/picture.jpg ~/backup/picture.jpg
	```


<p>...functions the same as the above command when it is run by boris.</p>
<h4>Copying Multiple Files To A Directory</h4>
<p>Or, perhaps you want to copy multiple files into another directory. To accomplish this, you can specify multiple files as the source, and a directory name as the destination. Let's say you are the user sally, and you have a bunch of files in the directory /home/sally/pictures/ named picture-01.jpg, picture-02.jpg... and you want to copy them into the directory /home/sally/picture-backup/. This command will do the trick</p>

	```shell
	$ cp ~/pictures/picture-*.jpg ~/picture-backup
	```


<p>Here, we use a wildcard (the asterisk, "*") to indicate that the source files are all the files in the directory /home/sally/pictures whose name starts with "picture-" and has the extension ".jpg". They will be copied into the directory /home/sally/picture-backup, assuming that directory already exists. If it doesn't exist, cp will give you an error message, and no files will be copied.</p>
<p>You can also specify multiple source files one after the other, and cp will expect that the final argument is a directory name, and copy them all there. For instance,</p>

	```shell
	$ cp ~/pictures/picture-01.jpg ~/pictures/picture-02.jpg ~/picture-backup
	```


<p>...will copy only those two files, /home/sally/picture-01.jpg and /home/sally/picture-02.jpg, into the directory /home/sally/picture-backup.</p>
<h4>Copying Files Recursively</h4>
<p>You can use cp to copy entire directory structures from one place to another using the -R option to perform a recursive copy. Let's say you are the user steve and you have a directory, /home/steve/files, which contains many files and subdirectories. You want to copy all those files, and all the subdirectories (and the files and subdirectories they contain), to a new location, /home/steve/files-backup. You can copy all of them using the command:</p>

	```shell
	$ cp -R ~/files ~/files-backup
	```


<p>...and the entire directory structure will be copied to the directory /home/steve/files-backup. When performing a recursive copy:</p>
<ul>
	<li>
	if the directory files-backup already exists, the directory files will be placed inside.</li>
	<li>if files-backup does not already exist, it will be created and the contents of the files directory will be placed inside it.</li>
</ul>
<h4>Creating Symbolic Links Instead Of Copying Data</h4>
<p>Another useful trick is to use cp to create symbolic links to your source files. You may already be familiar with using the ln command to create symlinks; cp is a great way to create multiple symlinks all at once.</p>
<p>cp will create symbolic links if you specify the -s option. So, for instance,</p>

	```shell
	$ cp -s file.txt file2.txt
	```


<p>...will create a symbolic link, file2.txt, which points to file.txt.</p>
<p>You can also create symbolic links from multiple source files, specifying a directory as the destination.</p>
<ul>
	<li>Note: To create symbolic links in another directory, cp needs you to specify the full pathname, including the full directory name, in your source filename(s). Relative paths will not work</li>
</ul>
<p>Let's say you are user melissa and you have a set of files, file01.txt, file02.txt... in the directory /home/melissa/myfiles. You want to create symbolic links to these files in the existing directory /home/melissa/myfiles2. This command will do the trick:</p>

	```shell
	$ cp -s ~/myfiles/file*.txt ~/myfiles2
	```


<p>The directory myfiles2 will now contain symbolic links to the file*.txt in the directory /home/melissa/myfiles. The myfiles2 directory must already exist for the operation to succeed; if it doesn't exist, cp will give you an error message and nothing will be copied.</p>
<p>This will work with a recursive copy, as well. So the command:</p>

	```shell
	$ cp -R -s ~/myfiles ~/myfiles2
	```


<p>...will re-create the directory structure of /home/melissa/myfiles, including any subdirectories and their contents; any files will be created as symlinks to the originals, but the directories will not be symbolic links, just regular directories. If myfiles2 already exists, cp will create a directory inside it called myfiles which contains the directory structure and symlinks; if myfiles2 does not already exist, it will be created, and contain the subdirectories and symlinks to the files that myfiles contains</p>
<p>There are many other options you can provide to cp which will affect its behavior. These are listed, along with the precise command syntax, in the following sections.</p>
<h4>Options</h4>
<p>Simply ask the terminal:</p>

	```shell
	$ cp --help
	```


<p>For the all the options available as well as more info</p>