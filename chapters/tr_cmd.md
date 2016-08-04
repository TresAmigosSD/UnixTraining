# Translate Command (tr)

The `tr` command allows the user to translate (map) characters in files from one value to another.

`tr` only accepts input from standard input and produces output on standard output.  User must provide redirection to specify input/output files (See [Redirect](redirect.md) for details).

## Mapping characters.

#### Simple character mapping
```bash
$ cat input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
...

$ tr ':' '|' < input_users.txt
USER_ID|ACCT_NUM|USER_NAME
3|5555|David
...
```

#### Character class mapping
```bash
# Map range ['a','z'] to range ['A','Z']
$ tr ‘[a-z]’ ‘[A-Z]’ < input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:DAVID
...

# same as above, but uses language independent classes.
tr ‘[:lower:]’ ‘[:upper:]’ < input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:DAVID
...
```

#### Deleting characters
`tr` can also be used to delete undesired characters.  The example below will delete all carriage returns from the dos file (effectively turning it into a unix format text file).

```bash
$ od -c -t x1 < dosfile.txt
0000000    h   e   l   l   o  \r  \n   b   y   e  \r  \n
           68  65  6c  6c  6f  0d  0a  62  79  65  0d  0a
0000014

$ tr -d '\r' < dosfile.txt | od -c -t x1
0000000    h   e   l   l   o  \n   b   y   e  \n
           68  65  6c  6c  6f  0a  62  79  65  0a
0000012
```
