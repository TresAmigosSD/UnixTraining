# Directory Commands

## Creating a Directory
`mkdir` command is used for creating a directory.

```bash
$ mkdir foo
$ ls -F
foo/
```

By default, `mkdir` does not allow the creation of a directory chain.  Each component of the directory chain must be created individually, unless the `-p` option is provided.
```bash
$ mkdir foo/bar/baz
mkdir: foo/bar: No such file or directory

$ mkdir -p foo/bar/baz
$ ls -F foo/bar
baz/
```

## Deleting Directory
To delete an empty directory:
```bash
$ rmdir empty_dir

$ rmdir foo
rmdir: foo: Directory not empty
```

To delete a directory and all its contents, use the `rm -rf` command. **Warning**: Use caution here!!!
```bash
$ rm -rf foo
```
