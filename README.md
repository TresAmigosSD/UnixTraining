# Unix Training For Data Scientists

This is a quick introduction to the most useful unix commands for folks doing data manipulation in a unix environment.  It is not a comprehensive introduction to Unix operating system (not even when constrained to topic at hand).

All files used in the examples are provided in the `files` directory of this repository.

For details explanation of the commands described in the following chapters, users should utilize the "man" command to show the manual page for a given command.  For example:
```bash
$ man grep
```
The above will show a detail manual page for the grep command.

## Text File Tranformation/Manipulation
* [Input/output redirection](redirect.md)
* [File hex dump](od_cmd.md)
* [Unix vs. Dos/Windows text files](dos_unix_files.md)
* [Translate characters](tr_cmd.md)
* [Removing funny/weird characters](funny_chars.md)
* [Searching files](grep_cmd.md)
* [Selecting columns from a file](cut_cmd.md)
* [Selecting top/bottom rows from a file](head_tail_cmd.md)
* [Counting lines in file](wc_cmd.md)
* [File difference](diff_cmp_cmd.md)
* [File checksum](checksum_cmd.md)
* [Sorting files](sort_cmd.md)
* [Joining files](join_cmd.md)

## Misc Commands
* [Finding/searching files across directories](find_cmd.md)
* [Directory commands](dir_cmds.md)
* [Timing Execution](time_cmd.md)

## General Purpose Data Manipulation "Languages"
* [AWK](awk_cmd.md)
* [SED](sed_cmd.md)
* [PERL](perl_cmd.md)
* [PYTHON](python_cmd.md)

## Remote Session Management / Connection
* [SSH](ssh_cmd.md)
* [TMUX](tmux_cmd.md)
* [SCREEN](screen_cmd.md)

## Virtualization Frameworks
* [DOCKER](docker.md)
* [Virtual Box](virtualbox.md)
