# AWK Command
The `awk` command is a general purpose stream processing application that is similar to [SED](sed_cmd.md).  However, `awk` can be used to generate much larger programs and is better at handling columnar data that is space separated.

This tutorial is not an exhaustive user guide for `awk`.  Only some useful tricks and tips that apply to data manipulation will be covered here.

## General Form
```bash
awk [-F _sep_] 'BEGIN {_init_action_} _pattern_ {_action_} ... END {_end_action_}'
```
* `_sep_` : an optional field separator can be specified as flag or using FS variable in BEGIN block.
* `_init_action_` : code specified inside the optional `BEGIN` special pattern is executed before any of the pattern matching occurs.  This is usually used to initialize counter variables, or print header columns.
* `_end_action_` : code specified inside the optional `END` special pattern is executed after all the pattern matching actions are performed.  This is usually used to print summary variables or table footers.
* `_pattern_` : a mathematical or regular expression.  The associated `_action_` is only executed for lines where `_pattern_` is true.  The awk program can contain one or more `_pattern_`/`_action_` pairs.

## Special Variables
The following variables are available inside the action blocks.
* `NR` : number of records seen so far.  Starts at 1.
* `NF` : number of fields in current record.
* `FS` : current input field separator (can be set using `-F` flag)

## Examples
Print columns 3 and 1 (in that order) from rows 2 to 4.  The pattern `2<=NR && NR<=4` will match rows 2 to 4 and only on these rows, will the print occur.  If the pattern was left blank, then the selected columns from all rows from the input will be shown.
```bash
$ awk -F: '2<=NR && NR<=4 {print $3"|"$1}' input_users.txt
David|3
Carol|5
Carol|11
```
----
print rows where the `ACCT_NUM` column (column #2) is even.  The expression `$2 % 2` will be 0 for even values and 1 for odd values of column 2.
```bash
$ awk -F: '$2%2 == 0 {print}' input_users.txt
USER_ID:ACCT_NUM:USER_NAME
1:1234:Frank
7:9876:Alice
4:666:Bob
11:1234:Carol
4:5566:Bob
```
----
Compute sum of ID column.  The column header "USER_ID" has a value of 0 when converted to numeric.
```bash
$ awk -F: 'BEGIN {SUM=0} {SUM+=$1} END {print "Sum of ID=",SUM}' input_users.txt
Sum of ID= 55
```
