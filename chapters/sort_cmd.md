# File Sorting

Text files can be sorted using numeric or lexical order by entire line or chosen columns.  The generic command is:

```bash
$ sort [-n] [-u] [-t sep] –k key1 [–k key2] file
```
* `-n`: use numeric sorting by default (can override per key)
* `-u`: only keep unique lines (remove duplicates)
* `-t`: specify the field separator for columns
* `-k`: specify one or more column sort order.  Each column spec can also override the numeric/lexical flag (`-n`)

## Examples
Lexical and numeric sort on entire line.  Note that records with `USER_ID` of 11 show up first lexically, but last numerically.
```bash
$ sort input_users.txt  | head -5
11:1234:Carol
11:5555:Carol
1:1234:Frank
2:123:Eric
3:5555:David

$ sort -n input_users.txt
USER_ID:ACCT_NUM:USER_NAME
1:1234:Frank
2:123:Eric
3:5555:David
4:5566:Bob
4:666:Bob
5:789:Carol
7:54321:Alice
7:9876:Alice
11:1234:Carol
11:5555:Carol
```

Get list of unique user id's
```bash
$ cut -f1 -d: < input_users.txt | sort -u -n
USER_ID
1
2
3
4
5
7
11
```

Sort by numeric account number (second column in input) and then by first column (numerically)
```bash
$ sort -k2n -k1n -t: input_users.txt
USER_ID:ACCT_NUM:USER_NAME
2:123:Eric
4:666:Bob
5:789:Carol
1:1234:Frank
11:1234:Carol
3:5555:David
11:5555:Carol
4:5566:Bob
7:9876:Alice
7:54321:Alice
```
