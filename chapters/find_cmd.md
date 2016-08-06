# Finding/Searching Files Across Directories
The `find` command is one of the most powerful Unix commands. It can be a bit difficult to master but with even just a couple of actions/filters, it can provide great power.

## `find` general format
```bash
$ find dir1 [dir2] ... _filters_ _actions_
```
* dirX : list of directory roots to search (e.g. `/`, `.`, `/home/me`)
* filters : set of filters to apply to select files to apply actions on.
* actions : set of actions to apply to filtered list of found files.

## Filters
#### Filter By Name
Find all "CSV" files in `/data` directory and all sub-directories.
```bash
$ find /data -name '*.csv'
```
#### Filter By Type
Find all directories under this sub-directory
```bash
$ find . -type d
```
Find all files under this sub-directory (ignores directories)
```bash
$ find . -type f
```
#### Filter By Modification Time
Find all files that have been modified in last 7 days.
```bash
$ find . -mtime -7 -type f
```

## Actions
#### Print
The simplest action is the default action which is to print the set of selected/found files. For Example, print name of all files/directories under current directory.
```bash
$ find . -print
```

#### Execute
Use the `-exec cmd ... \{\} +` action to run a command on the filtered set of found files.
```bash
$ find . -name '*file.txt' -exec echo "XXX" \{\} "YYY" +
XXX ./dosfile.txt ./unixfile.txt
```

## Real Examples
Find all java files in both source and test directories that have been modified in the last 2 days
```bash
$ find ./src ./test -name '*.java' -mtime -7 -print
./src/com/company/proj/a.java
./test/com/company/proj/x.java
...
```
----
Count number of lines in all the text files in current directory (and sub-directories)
```bash
$ find . -name '*.txt' -exec wc -l \{\} +
       2 ./dosfile.txt
      11 ./funnychars.txt
      11 ./input_users.txt
       0 ./invisible_bytes.txt
       2 ./unixfile.txt
      26 total
```
----
Find name of all CSV files that contain the account number "12345678"
```bash
$ find /data -name '*.csv' -exec grep -l "12345678" \{\} +
```

If we wanted to show the actual matching lines from above, we would remove the `-l` flag.
```bash
$ find /data -name '*.csv' -exec grep "12345678" \{\} +
```
----
Find 5 largest files in current directory (See [Sort](sort_cmd.md))
```bash
$ find . -type f -exec du -s \{\} + | sort -k1,1nr | head -5
16192	./target/scala-2.10/smv-1.5-SNAPSHOT-jar-with-dependencies.jar
8240	./tools/template/data/input/employment/CB1200CZ11.csv
7784	./.git/objects/pack/pack-ee67150bd1271b8415d717022c952a913034efb0.pack
7600	./target/streams/test/incCompileSetup/$global/streams/inc_compile_2.10
5056	./target/streams/$global/update/$global/streams/out
```
