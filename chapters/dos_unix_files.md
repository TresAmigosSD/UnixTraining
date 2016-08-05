# Unix vs. Dos/Windows Text Files

Text files on Unix and Windows look similar but they usually use a different line ending.  Most modern unix tools ignore this difference and can handle either line ending.  However, users sometimes can run into an issue due to using dos/windows text files on unix.

## Unix/Dos text file contents.

Looking at the two provided sample files using cat:
```bash
$ cat unixfile.txt
hello
bye

$ cat dosfile.txt
hello
bye
```

The two files appear identical.  However, looking at the actual bytes using the [Octal Dump Cmd](od_cmd.md) tells another story.

```bash
$ od -c -t x1 unixfile.txt
0000000    h   e   l   l   o  \n   b   y   e  \n
           68  65  6c  6c  6f  0a  62  79  65  0a
0000012

$ od -c -t x1 dosfile.txt
0000000    h   e   l   l   o  \r  \n   b   y   e  \r  \n                
           68  65  6c  6c  6f  0d  0a  62  79  65  0d  0a
0000014
```

## Converting between Unix/Dos text file formats

The `dos2unix` and `unix2dos` commands can be used to convert a file to the desired line ending format.  They do the replacement "in-place"

```bash
$ dos2unix dosfile.txt
$ od -c -t x1 dosfile.txt
0000000   h   e   l   l   o  \n   b   y   e  \n
         68  65  6c  6c  6f  0a  62  79  65  0a
0000012
```

If the above commands are not available, the [TR](tr_cmd.md) command can be used to do the same.
```bash
$ tr -d '\r' < dosfile.txt > unixfile.txt
```

## Other file encodings

TODO: describe UTF8, code pages, etc and the iconv command.
