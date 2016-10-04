# Understand and Change File Permissions

Unix file system handles access control of files and directories though "permissions".

There are 3 basic types of permissions:
* Read: represent by letter "r"
* Write: represent by letter "w"
* Executable: represent by letter "x"

There 3 subjects which can be granted permissions of a file to:
* Owner: the file owner himself/herself
* Group: all users who are in the group of the file
* Others: everyone else

When one use `ls -l` command to list a file, he will get a string which shows the permissions
```shell
$ ls -l files/dosfile.txt
-rw-rw-r-- 1 ninjapapa staff 10 Oct  4 12:29 files/dosfile.txt
```

Here
* `ninjapapa` is the owner name: the file own by `ninjapapa`
* `staff` is the group name: the file belongs to `staff` group (the user must be in that group)
* `-rw-rw-r--` represent the permissions on the 3 subjects.

`-rw-rw-r--` basically means that the file has
* Owner has Read and Write permissions
* Group has Read and Write permissions
* Others have Read only permission

## Change permissions
The owner of a file or administrators (super user) can change the permissions of a file. Here are
some examples:

Add execution permission for everyone on a file,
```shell
$ chmod a+x myscript.py
```

Remove write permission from Group and Others,
```shell
$ chmod go-w files/dosfile.txt
```

Add read permission for Group and Others for all the files under a directory,
```shell
$ chmod -R go+r files
```

## Further study
Please do `man chmod` to learn more options of the command.

Also sometimes you may want to change file ownership. Command `chown` is for that. Please
do `man chown` to learn more on it.

Some advanced topics about Unix permissions which are not covered:
* Use `umask` to control the default permissions for any newly created file
* Use octal number to set permissions
* `s` and `t` permission symbols
