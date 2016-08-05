# Searching files using grep commands

The `grep` command is used to search the contents of a given file(s) for a pattern.  It will display all lines of the file that contain the given search pattern.

The general format is:
```bash
$ grep [-v] [-i] [-E] _pattern_ _file1_ ...
```

* `-v` : reverse the search.  only show **Non Matching** lines.
* `-i` : ignore case in comparing pattern to file contents.
* `-E` : use regular expressions for matching patterns.
* `_pattern_` : search pattern.

## Examples

#### Simple match
```bash
$ grep Alice input_users.txt
7:9876:Alice
7:54321:Alice
```

#### Case insensitive search
```bash
# no lines match lower-case "alice"
$ grep alice input_users.txt

$ grep -i alice input_users.txt
7:9876:Alice
7:54321:Alice
```

#### Reverse search
Show all lines that do not match the given pattern.
```bash
$ grep -v Alice input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Carol
...
```

#### Regular expression search
```bash
$ grep -E '(Frank|Alice)' input_users.txt
1:1234:Frank
7:9876:Alice
7:54321:Alice
```
