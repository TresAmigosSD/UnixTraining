# File Checksum

The situation arises often when we need to determine of two files on different systems are the same.  We can copy them to a single system and perform a `cmp` as desribed in [File difference](chapters/diff_cmp_cmd.md).  However, this could be quite expensive if the files are large.  An alternative is to compute the checksum of the files and we can be fairly certain that they files are the same if their checksum is the same.

## Examples
Compute checksum using common built-in commands in Linux/Unix
```bash
$ sum input_users.txt
53205 1 input_users.txt

$ cksum input_users.txt
2392506273 152 input_users.txt

$ md5 input_users.txt
MD5 (input_users.txt) = 1ab22f1e669c479ad4d0d636061e7097
```

If `openssl` is installed, it can be used to generate checksum for various digest algorithms.
```bash
$ openssl dgst -sha1 input_users.txt
SHA1(input_users.txt)= 0af97bfc3706309311b32f3bee8d25c2f83312ff

$ openssl dgst -sha256 input_users.txt
SHA256(input_users.txt)= eb72d432966e19c8cd742e618e1e0c7e9691912b22cc8a05fe9dce70f2f9e7d7

$ openssl dgst -md5 input_users.txt
MD5(input_users.txt)= 1ab22f1e669c479ad4d0d636061e7097
```
