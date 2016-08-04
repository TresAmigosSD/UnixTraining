# Unix Command Input/Output redirection

Most "filter" type Unix commands will read from standard input and write to standard output.  The default behavior can be modified in the shell when the command is executed.

## Output redirection
In the example below, the contents of the `unixfile.txt` file are first dumped to standard output (screen) and then redirected to another file.

```bash
$ cat unixfile.txt
hello
bye

$ cat unixfile.txt > tmpfile

$ cat tmpfile
hello
bye
```

## Input redirection
The input can also be redirected.
```bash
$ cat < unixfile.txt
hello
bye
```

## Chaining commands.
Unix is built on the philosophy that each command should be simple and do only one thing but do it well.  Piping is used to chain these simple commands to create complex workflows.

For example, to see how many lines in the file `input_users.txt` contain the word Alice, we would run the following.
```bash
$ cat input_users.txt  | grep Alice | wc -l
    2
```

The above will "pipe" the output of the `cat` command to the input of the `grep` command then "pipe" the output of the `grep` command to the input of the `wc` command.

See [grep](grep_cmd.md) and [wc](wc_cmd.md) for details about the above commands used in the pipe.
