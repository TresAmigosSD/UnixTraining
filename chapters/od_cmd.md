# Octal Dump Command (od)

The Octal Dump (od) command allows the user to see the raw bytes contained in the file.  The example file `invisible_bytes.txt` contains a "hidden" characters that can not be see with a simple `cat` command.

```bash
$ cat invisible_bytes.txt
hithere

$ od -c -t x1 invisible_bytes.txt
0000000    h   i  \0   t   h   e   r   e                                
           68  69  00  74  68  65  72  65                                
0000010
```

The `-c` tells `od` to output non-printable characters as C-escaped characters and the `-t x1` will output the contents of the file as hexadecimal bytes (much easier to understand than the default octal).

With the hex dump, we are able to see the hidden `\0` (ASCII 0) byte between `hi` and `there`.
