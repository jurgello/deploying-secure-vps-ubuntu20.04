# Chmod codes cheat sheet

### How to use chmod codes in UNIX:

1. There are three types of permissions in files and folders in unix
    1. Read    (**r**)
    2. Write   (**w**)
    3. Execute (**x**)
2. And, there is a classification of users called UGO (explained bellow):
    1. **U** ~> User (usually, you)
    2. **G** ~> Group (eg sudo group)
    3. **O** ~> Others

When you run `$ ls -l` your output will be something like this:

```
-rwxrwxrwx@  1 user  staff  708301983 Aug 11 13:51 all.zip
-rw-r--r--   1 user  staff          0 Aug 22 22:10 chmodCheatSheet.md
-r--------@  1 user  admin       1692 Jul  6 10:13 deploykey.pem
drwxr-xr-x   3 user  staff        102 Aug 20 19:14 deploynode
```

### How to read this?

Where is a letter put a `1` and where is a `-` put a `0`. Examples:

| **U**        | **G**           | **O**  |
| ------------- |:-------------:| -----:|
| r w x| r w x | r w x |
|1 1 1 | 1 1 1 | 1 1 1|

So, user, group and others can read, write and excute the file or folder


| **U**        | **G**           | **O**  |
| ------------- |:-------------:| -----:|
| r w -| r -- | r - x |
|1 1 0 | 1 0 0 | 1 0 1|

So, user can read and write, group can only read, finally other can read and execute

#### As you can see, we can play with these permissions

| **U**        | **G**           | **O**  |
| ------------- |:-------------:| -----:|
| r - x| r w - | - - - |
|1 0 1 | 1 1 0 | 0 0 0|
| **U**        | **G**           | **O**  |
| - w x| r - x | - - x |
|0 1 1 | 1 0 1 | 0 0 1|

### Finally, the codes! (sorry)

| Bin        | Decimal           | Representation  |
| ------------- |:-------------:| -----:|
| 000      | 0 | -&nbsp;-&nbsp;- |
| 001      | 1 |   -&nbsp;-&nbsp;x |
| 010 | 2 |    -&nbsp;w&nbsp;- |
| 011 | 3 |    -&nbsp;w&nbsp;x |
| 100 | 4 |    r&nbsp;-&nbsp;- |
| 101 | 5 |    r&nbsp;-&nbsp;x |
| 110 | 6 |    r&nbsp;w&nbsp;- |
| 111 | 7 |    r&nbsp;w&nbsp;x |

The syntax is something like this: `$ chmod u/permissions g/permissions o/permissions file[or /dir/]`

* So, if I run `$ chmod 777 file` <=>
`rwx rwx rwx` everybody can do anything with **file**
* Or I run `$ chmod 744 dir` <=>
`rwx r-- r--`only user can read, write and execute, group and others only read **dir**. 
* Or run `$ chmod 200 file2` <=>
`-w- --- ---`only you can write **file2**

Thanks for reading, I hope it works! Follow me on [Twita](https://twitter.com/soyjuanarbol) and [GitHub](https://github.com/juanarbol)

Refs:
1. http://www.pa.msu.edu/~abdo/unixcc.html
2. http://www.yourownlinux.com/2013/09/chmod-basics-of-filesdirectories.html