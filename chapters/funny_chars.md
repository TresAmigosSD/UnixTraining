# Non-Printable (funny) chars in files.

There are times when files contain spurious Non-Printable characters.  These can be due to conversion errors or the files are actually in different encoding (See "Encoding" section in the [Unix vs. Dos/Windows text files](chapters/dos_unix_files.md) chapter).

People often provide "CSV" (Comma Separated Values) files with a Non-Printable field separator.  For example:

```bash
$ cat funnychars.txt | head -4
USER_IDACCT_NUMUSER_NAME
35555David
5789Carol
15555Carol

$ od -c -t x1 funnychars.txt | head -4
0000000    U   S   E   R   _   I   D 001   A   C   C   T   _   N   U   M
           55  53  45  52  5f  49  44  01  41  43  43  54  5f  4e  55  4d
0000020  001   U   S   E   R   _   N   A   M   E  \n   3 001   5   5   5
           01  55  53  45  52  5f  4e  41  4d  45  0a  33  01  35  35  35
```

We will utilize the [TR](tr_cmd.md) to translate the Non-Printable separator (ASCII 01) into a `:` character.

```bash
$ cat funnychars.txt | head -4 | tr '\1' ':'
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Carol
1:5555:Carol
```
