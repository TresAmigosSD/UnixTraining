# Stream Editor (sed) command

`sed` can be used to edit text/files "in-stream".  It is quite handy in a chain of piped commands.  The general format of the `sed` command is:
```bash
$ sed [-n] [-e 'line_range action' ...] < input > output
```

* `-n` : Suppress default behavior to output all input lines.
* `-e` : Execute the following line range and action combination.  A single `sed` command may have multiple `-e` flags.
* `line_range` : specify the lines to take action upon in form of "start_line,endline".  For example, `3,5` means lines 3 through 5 inclusively. If `line_range` is blank, it means the action applies to all alines in input.
* `action` : the action to take.  The two most common actions are:
 * `p` : print the line (usually combined with `-n` command line flag)
 * `s/regex/new_value/g` : substitute all matching `regex` values with the given new value. See "Common Regex Patterns" section below.

## Examples
Display lines 2 to 4 from `input_users.txt`
```bash
$ sed -n -e '2,4p' input_users.txt
3:5555:David
5:789:Carol
11:5555:Carol
```

Substitute all occurrences of "Carol" with "Susan".
```bash
$ sed -e 's/Carol/Susan/g' input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Susan
11:5555:Susan
1:1234:Frank
7:9876:Alice
4:666:Bob
7:54321:Alice
2:123:Eric
11:1234:Susan
4:5566:Bob
```

Only do the above substitution on lines 1-3.
```bash
$ sed -e '1,3s/Carol/Susan/g' input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Susan
11:5555:Carol
1:1234:Frank
7:9876:Alice
4:666:Bob
7:54321:Alice
2:123:Eric
11:1234:Carol
4:5566:Bob
```

Quote all numbers in file.  The pattern `[0-9][0-9]*` will match one or more digits and since the pattern is enclosed in `\(\)`, it will be substituted in the output by the `\1` marker.
```bash
$ sed -e 's/\([0-9][0-9]*\)/"\1"/g' input_users.txt
USER_ID:ACCT_NUM:USER_NAME
"3":"5555":David
"5":"789":Carol
"11":"5555":Carol
...
```

Convert `:` field separator to `|`.
```bash
$ sed -e 's/:/|/g' input_users.txt
USER_ID|ACCT_NUM|USER_NAME
3|5555|David
5|789|Carol
11|5555|Carol
1|1234|Frank
7|9876|Alice
4|666|Bob
7|54321|Alice
2|123|Eric
11|1234|Carol
4|5566|Bob
```

Add a column to the beginning and end of each line.  The `^` and `$` pattern match the beginning and end of line respectively.
```bash
$ sed -e 's/^/BAR:/' -e 's/$/:FOO/' input_users.txt
BAR:USER_ID:ACCT_NUM:USER_NAME:FOO
BAR:3:5555:David:FOO
BAR:5:789:Carol:FOO
BAR:11:5555:Carol:FOO
BAR:1:1234:Frank:FOO
BAR:7:9876:Alice:FOO
BAR:4:666:Bob:FOO
BAR:7:54321:Alice:FOO
BAR:2:123:Eric:FOO
BAR:11:1234:Carol:FOO
BAR:4:5566:Bob:FOO
```
## Common Regex Patterns.
<table>
 <tr>
  <th>Regex</th>
  <th>Description</th>
  <th>Example</th>
 </tr>
 <tr>
  <td>`^`</td>
  <td>Anchor to beginning of line</td>
  <td>`^abc`</td>
 </tr>
 <tr>
  <td>`$`</td>
  <td>Anchor to end of line</td>
  <td>`xyz$`</td>
 </tr>
 <tr>
  <td>`[...]`</td>
  <td>matches set of characters and ranges</td>
  <td>`[abc]` : matches 'a' or 'b' or 'c'<br>`[0-9a-z]` : matches all digits and lowercase letters.</td>
 </tr>
 <tr>
  <td>`[^...]`</td>
  <td>negates match of characters/ranges</td>
  <td>`[^abc]` matches anything other than 'a','b', or 'c'</td>
 </tr>
 <tr>
  <td>`.`</td>
  <td>Matches any single character.</td>
  <td>`a.c` : matches 'abc', 'aac', or any three characters that start with 'a' and end with 'c'</td>
 </tr>
 <tr>
  <td>`*`</td>
  <td>matches 0 or more instances of previous character.</td>
  <td>`[0-9]*` match 0 or more digits</td>
 </tr>
 <tr>
  <td>`+`</td>
  <td>matches 1 or more instances of previous character.</td>
  <td>`[0-9]+` match 1 or more digits</td>
 </tr>
 <tr>
  <td>`{n,m}`</td>
  <td>matches n to m instances of previous character.  Both n and m are optional and default to 0 and infinite respectively</td>
  <td>`[0-9]{3,5}` : match 3 to 5 digits.<br>`[0-9]{,4}` : match 0 to 4 digits.<br>`[0-9]{2,}` : match 2 or more digits.</td>
 </tr>
</table>
