# File Difference

## Diff Command
`diff` can be used to show the difference between two files / directories at the line level.
The general format is:
```bash
$ diff [-i] [-w] [-r] file1 file2
```
* `-i` : ignore case when comparison.
* `-w` : ignore all whitespace in comparison.
* `-r` : recursively compare all files in directories rather than just individual files.

#### Examples
The Example below uses `diff` with default flags (case and whitespace are significant).  Lines starting with `<` indicate lines from the first file, while lines starting with `>` indicate the second file.  We see three types of changes:
* `David` has been changed to `david`
* A couple of the `Alice` and `Bob` lines have been prefixed with spaces.
* `Eric` only exists in `input_users.txt` and `George` only exists in `output_users.txt`

```bash
$ diff input_users.txt output_users.txt
2c2
< 3:5555:David
---
> 3:5555:david
6,7c6,7
< 7:9876:Alice
< 4:666:Bob
---
>   7:9876:Alice
>   4:666:Bob
9d8
< 2:123:Eric
10a10
> 9:628:George
```

If we re-run the above command but disable checks for whitespace (`-w`) and ignore case (`-i`), we only see the added/removed lines.

```bash
$ diff -i -w input_users.txt output_users.txt
9d8
< 2:123:Eric
10a10
> 9:628:George
```

`diff` can also be used to recursively compare the contents of two directories

```bash
$ diff -r dir1 dir2
```

## Cmp command
While `diff` does comparison at the line level, `cmp` compares files at the byte level.  It is often much quicker to do a `cmp` when trying to determine if two files have the same content or not.

```bash
$ cmp -b input_users.txt output_users.txt
input_users.txt output_users.txt differ: byte 35, line 2 is 104 D 144 d
```
