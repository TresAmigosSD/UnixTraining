# Timing Command Execution

`time` command can be used to time the execution of any unix command.  For example,

```bash
$ time grep 1234 input_users.txt
1:1234:Frank
11:1234:Carol

real	0m0.004s
user	0m0.001s
sys	0m0.002s
```

The `real` time is the wall clock time while `user`/`sys` times are internal user and system times.
