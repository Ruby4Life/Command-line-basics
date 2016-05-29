scp syntax:
```shell
$ scp [-12346BCEpqrv] [-c cipher] [-F ssh_config] [-i identity_file] [-l limit] [-o ssh_option] [-P port] [-S program] [[user@]host1:]file1 ... [[user@]host2:]file2
```


Explaining the complete syntax and every option of this command is out of the scopy of this page, you can always enter a the command prompt
```shell
$ man scp
```
Or you can read it online here

We are going to explain the basic part of it:
```shell
$ scp [[user@]host1:]file1 ... [[user@]host2:]file2
```

scp:
    Is the command itself and tells the operating system to copy one or more files over a secure shell connection, better known as ssh connection.
[[user@]host1:]file1
    The origin, where you specify the file or files to be copied, it can contain or not the information about a remote host, and it can also contain the information about the user owning the file or files in that remote host. If the user is not specified it will defaults to the current user in the machine where you are typing the command. If the host is not specified, it will look for the file locally using any given path.
[[user@]host2:]file2
    The destination, where you specify the path where the files are going to be copied, once again, it can contain or not the information about the remote host and/or user in that host. Same as above if the user is not specified but a hostname is given it will defaults to the current username and will try to log in the remote server using that user. And in the same way as with origin, if the host is not specified, the files will be copied locally.

Just to clarify, you can avoid specifying both username and host in origin and destination, and the scp command will work just like the cp command, copying a local file to a local destination.
Examples

Copy one single local file to a remote destination
```shell
$ scp /path/to/source-file user@host:/path/to/destination-folder/
```

So, if you wan to copy the file /home/user/table.csv to a remote host named host.example.com and copy there to jane's home folder, use this command.
```shell
$ scp /home/user/table.csv jane@host.example.com:/home/jane/
```

Copy one single file from a remote server to your current local server
```shell
$ scp user@host:/path/to/source-file /path/to/destination-folder
```

Let's say now you want to copy the same file from jane's home folder in host.example.com to your local home folder.
```shell
$ scp jane@host.example.com:/home/jane/table.csv /home/user/
```

Copy one single file from a remote server to another remote server

With scp you can copy files between remote servers from a third server without the need to ssh into any of them, all weight lifting will be done by scp itself.
```shell
$ scp user1@server1:/path/to/file user2@server2:/path/to/folder/
```

Let's say now you want to copy the same table file from jane's home folder to pete's home folder in another remote machine.
```shell
$ scp jane@host.example.com:/home/jane/table.csv pete@host2.example.com:/home/pete/

Copy one single file from a remote host to the same remote host in another location
```shell
$ scp jane@host.example.com:/home/jane/table.csv pete@host.example.com:/home/pete/
```

This time, you will be copying from one host to the same host, but on different folders under the control of different users.

Copy multiple files with one command

You can copy multiple files at once without having to copy all the files in a folder, or copy multiple files from different folders putting them in a space separated list.
```shell
$ scp file1.txt file2.txt file3.txt pete@host.example.com:/home/pete/
```

If the files are in different folders, just specify the complete path.
```shell
$ scp /path/to/file1.txt /path/to/file2.txt /path/to/file3.txt pete@host.example.com:/home/pete/
```

Copy all files of a specific type
```shell
$ scp /path/to/folder/*.ext user@server:/path/to/folder/
```

This will copy all files of a given extension to the remote server. For instance, you want to copy all your text files (txt extension) to a new folder.
```shell
$ scp /home/user/*.txt jane@host.example.com:/home/jane/
```

You can make use of wildcards in any way you want.

Copy all files in a folder to a remote server
```shell
$ scp /path/to/folder/* user@server:/path/to/folder/
```

This will copy all files inside local folder to the remote folder, let's see an example.
```shell
$ scp /home/user/html/* jane@host.example.com:/home/jane/backup/
```

All files in local folder html, will be copied to backup folder in host.example.com

Copy all files in a folder recursively to a remote server
```shell
$ scp -r /home/user/html/* jane@host.example.com:/home/jane/backup/
```

Same as the previous example, but this time it will copy all contentes recursively

Copy a folder and all its contents to a remote server
```shell
$ scp -r /path/to/source-folder user@server:/path/to/destination-folder/
```

This time the folder itself is copied with all its contents and not only the contents. One more time we'll use an example.
```shell
$ scp -r /home/user/html jane@host.example.com:/home/jane/backup/
```

This will result in having in the remote server this: /home/jane/backup/html/.... The whole html folder and its contentes recursively have been copied to the remote server.
Tips

We have seen the basic uses scp, now we will see some special uses and tricks of this great command

Increase Speed

scp uses AES-128 to encrypt data, this is very secure, but also a litle bit slow. If you need more speed and still have security, you can use Blowfish or RC4.

To increase scp speed change chipher from the default AES-128 to Blowfish
```shell
$ scp -c blowfish user@server:/home/user/file .
```

Or use RC4 which seems to be the fastest
```shell
$ scp -c arcfour user@server:/home/user/file .
```

This last one is not very secure, and it may not be used if security is really an issue for you.

Increase Security

If security is what you want, you can increase it, you will lose some speed though.
```shell
$ scp -c 3des user@server:/home/user/file .
```
Limit Bandwidth

You may limit the bandwidth used by scp command
```shell
$ scp -l limit username@server:/home/uername/* .
```
Where limit is specified in Kbit/s. So for example, if you want to limit speed at 50 Kbps
```shell
$ scp -l50 user@server:/path/to/file /path/to/folder
```
Save Bandwidth

Yoy can save bandwidth by enabling compression, let's see our example with compression.
```shell
$ scp -C user@server:/path/to/file /path/to/folder
```
Use IPv4 or IPv6

If you want to force the use of either IPv4 or IPv6 use any of these ones.
```shell
$ scp -4 user@server:/path/to/file /path/to/folder
```
The above one is for IPv4, and below for IPv6.
```shell
$ scp -6 user@server:/path/to/file /path/to/folder
```
Specify a port

If the remote server does not have ssh listening on default 22 port, you can make scp to use the port where the remote server is listening to:
```shell
$ scp -P [port] [user]@[server]:[path/to/]file [/path/to/]file
```
Using the capital letter P you can make scp to use a port other than 22 which is the default for ssh. Let's say your remote server is listening on 2222.
```shell
$ scp -P 2222 user@server:/home/jane/file /home/jane/
```
Use verbose output

If you want to see what is happening under the hood, use the -v parameter for a verbose output
```shell
$ scp -v user@server:/home/jane/file /home/jane/
```
