# Filtering for top/bottom rows of a file (head/tail)

## Head
Use `head -n` to show the first N lines of a file.
```bash
$ head -n3 input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Carol
```
Most implementations also allow use without `-n`
```bash
$ head -3 input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Carol
```

## Tail
Similar to `head` but shows bottom of file.
```bash
$ tail -n3 input_users.txt
2:123:Eric
11:1234:Carol
4:5566:Bob
```

If `tail` is given a number in the format of `+N`, it will show the file starting at line `N` to the end.  Combining the above, we can show lines 2-4 (skip header and show first 3 lines of actual data) as follows:
```bash
$ tail -n +2 input_users.txt | head -3
3:5555:David
5:789:Carol
11:5555:Carol
```

## Continuous Tail
`tail -f` will continuously poll the file for new output.  This is useful for monitoring the output of a long running process.
```bash
# In some other shell or in background:
$ long_running_program .. > program_output

$ tail -f program_output
```
