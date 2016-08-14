# Perl interpreter
`perl` can be considered a general purpose programming language. A full tutorial on `perl` is beyond the scope of this tutorial.  Only some useful tools and one liners will be introduced here.

While `perl` is a bit more difficult to master than `awk`, it can often do things at much faster rate.  So it is handy to use on large files even if the same task can be done in `awk`.

## Simple program run
`perl` programs can be provided on the command line directly without creating a separate program file.  The `-e` flag is used to indicate that the program code is to follow.  For example:
```bash
$ perl -e 'print "hello world\n"'
```

## Automatic file loop
Since we will be using `perl` for data processing, we will often rely on the `-p` and `-n` flags.  These flags will automatically loop over all lines in files specified on command line or standard input and run the provided code over them.  `-p` will also print the line after processing, while `-n` would require the user to print the line (useful if you only want to print certain lines).

In the example below, we will prepend and append a character to each line in the input.  Note that unlike `awk`, `perl` will *NOT* remove the trailing new line from each line.  Hence, we must use `chomp` method to remove the trailing new line.  By default, most methods in `perl` operate on the `$_` operator and hence we don't need to specify that as an argument to `chomp`.
```bash
$ perl -n -e 'chomp; print "X $_ X\n"' input_users.txt
X USER_ID:ACCT_NUM:USER_NAME X
X 3:5555:David X
X 5:789:Carol X
...
```
----
If we are only transforming rows in input, then we can rely on the `-p` flag and its automatic printing.
```bash
$ perl -p -e 's/Carol/Susan/' input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Susan
11:5555:Susan
...
```
The above works because the `s/../../` substitution command reads/writes to `$_` by default and the `-p` automatic print displays `$_`.  We could also modify `$_` directly as part of the program:
```bash
$ perl -p -e '$_ = "X" . $_' input_users.txt
XUSER_ID:ACCT_NUM:USER_NAME
X3:5555:David
X5:789:Carol
X11:5555:Carol
...
```

## Auto field split
When working with columnar (CSV) data, it is often handy to use the `-a` auto-split command line option.  This option will split each input line and store the split array in `@F`.  The `-F` flag can be used to specify the field separator.
```bash
$ perl -F':' -ane 'print "$F[1]\n"' input_users.txt
ACCT_NUM
5555
789
5555
...
```

## BEGIN/END blocks
Similar to `awk`, `perl` also supports the special `BEGIN`, `END` blocks to indicate code that needs to run at the beginning and end of processing respectively.

The example below will produce the sum of all values in column 2 (`$F[1]`).  Note that if a `BEGIN` and/or `END` block is present, we need to enclose the normal code in `{}`.  Also note that we did not need to initialize `$s` to zero in a `BEGIN` block.
```bash
$ perl -F':' -an -e '{$s += $F[1]}' -e 'END {print "sum = $s\n"}' input_users.txt
sum = 84919
```

## In-place file modification
It is often required to modify the contents of a file rather than create a new file.  `perl` makes this quite easy with the `-i` flag.
```bash
$ cp input_users.txt x.txt
$ perl -pi -e 's/Frank/Fred/' x.txt
$ diff input_users.txt x.txt
5c5
< 1:1234:Frank
---
> 1:1234:Fred
$ rm x.txt
```

It is also possible to create a backup of the original file before it is replaced:
```bash
$ perl -p -i.bak -e 's/Frank/Fred/' x.txt
```

## Special Variables
TODO: document common special variables (e.g. `$_`, `$/`, ...)

## Links
* [perl command line options](http://www.perl.com/pub/2004/08/09/commandline.html)
* [Collection of perl one liners](http://www.math.harvard.edu/computing/perl/oneliners.txt)
