# Unix Training For Data Scientists

This is a quick introduction to the most useful unix commands for folks doing data manipulation in a unix environment.  It is not a comprehensive introduction to Unix operating system (not even when constrained to topic at hand).

All files used in the examples are provided in the `files` directory of this repository.

For details explanation of the commands described in the following chapters, users should utilize the "man" command to show the manual page for a given command.  For example:
```bash
$ man grep
```
The above will show a detail manual page for the grep command.

## Text File Tranformation/Manipulation
* [Input/output redirection](chapters/redirect.md)
* [File hex dump](chapters/od_cmd.md)
* [Unix vs. Dos/Windows text files](chapters/dos_unix_files.md)
* [Translate characters](chapters/tr_cmd.md)
* [Removing funny/weird characters](chapters/funny_chars.md)
* [Searching files](chapters/grep_cmd.md)
* [Selecting columns from a file](chapters/cut_cmd.md)
* [Selecting top/bottom rows from a file](chapters/head_tail_cmd.md)
* [Counting lines in file](chapters/wc_cmd.md)
* [File difference](chapters/diff_cmp_cmd.md)
* [File checksum](chapters/checksum_cmd.md)
* [Sorting files](chapters/sort_cmd.md)

## Misc Commands
* [Finding/searching files across directories](chapters/find_cmd.md)
* [Directory commands](chapters/dir_cmds.md)
* [Timing Execution](chapters/time_cmd.md)

## General Purpose Data Manipulation "Languages"
* [AWK](chapters/awk_cmd.md)
* [SED](chapters/sed_cmd.md)
* [PERL](chapters/perl_cmd.md)
* [PYTHON](chapters/python_cmd.md)

## Hadoop Commands
* [Hadoop filesystem](chapters/hdfs.md)
* [Yarn commands](chapters/yarn.md)

## Remote Session Management / Connection
* [SSH](chapters/ssh_cmd.md)
* [TMUX](chapters/tmux_cmd.md)
* [SCREEN](chapters/screen_cmd.md)

## Virtualization Frameworks
* [DOCKER](chapters/docker.md)
* [Virtual Box](chapters/virtualbox.md)
