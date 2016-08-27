# Command Shell

Current common shells today are quite powerful.  However, it is incumbent upon the developer to create aliases and scripts for often repeated tasks.  This tutorial assumes user is using `bash`. Any other modern shell should have similar functionality.

## Environment Variables
Most environment variables are either set by the global config or set in the users `~/.bash_profile` or `~/.bashrc` files.  If an environment variable is modified in these files, then the file needs to sourced again to pick up the changes.  For example:
```bash
$ source ~/.bashrc
```
#### Common Environment Variables
<table>
<tr>
  <th>ENV</th>
  <th>Description</th>
</tr>
<tr>
  <td>PATH</td>
  <td>`:` separated list of directories to search for executables</td>
</tr>
<tr>
  <td>HOME</td>
  <td>Home directory of current user</td>
</tr>
<tr>
  <td>USER</td>
  <td>Current user name</td>
</tr>
<tr>
  <td>PWD</td>
  <td>Current working directory.  Can also use `$(pwd)`</td>
</tr>
</table>

```bash
$ echo $HOME
/Users/alitajeldin
```

## Aliases
Aliases allow user to create shortcuts for common tasks.  For example, the maven command to build a project and skip tests is `mvn clean install -DskipTests`.  Remembering and typing this command every time is error prone.  Instead, it is best to create an alias:
```bash
$ alias mcit='mvn clean install -DskipTests'
```
Henceforth, typing `mcit` will run the full maven command.  To avoid having to repeatedly define the alias, the alias defintion should go in `~/.bash_profile` or `~/.bashrc` so that it is defined for every shell.

It is good practice to create aliases for common commands and directory navigation.  For example:
```bash
alias ll='ls -l'
alias lh='ls -lh'

alias gop='cd /home/user/projects/myproject'

alias mci='mvn clean install'
alias mcit='mvn clean install -DskipTests'
```
## Functions
Aliases are limited to static content.  For parameterized aliases, one must resort to functions.  The general format is:
```bash
function func_name() {
  _function_body_
}
```

Inside the function body, user has access to the arguments, aliases, and environment variables.  The arguments can be accessed as `$@` for all the argument or `$1`..`$9` for the nth argument.  For example:
```bash
function hello() {
  echo How are you $1
}
function howdy() {
  echo How are you $@
}

$ hello Bob Fred
How are you Bob
$ howdy Bob Fred
How are you Bob Fred
```
Note how the `hello` function only echos the first argument, while the `howdy` function echos all the arguments.

#### Function Examples
```bash
# sets the docker environment to point to given docker instance
# Example: dme default
function dme(){
    eval $(docker-machine env $1)
}

# print first 5 lines of all specified files.
# Example: headall file1 file2
# Note: this is equal to head -5 file1 file2 (this is jsut for demonstration purposes)
$ function headall() {
   for f in $@; do
     echo $f
     head -5 $f
   done
}
```

#### Complex Function Example
Body of function can utilize other functions and aliases.  The example below defined the `ip_from_instance` function that will determine the AWS public instance IP, given the instance tag name.  The function needs to be called with two arguments.  First, the tag name and second the tag value (e.g. `ip_from_instance Name foo`) will find the ip of instance named `foo`.  The `ssh-aws-name` function uses the `ip_from_instance` function to get the public ip of machine to connect to.
```bash
# $1 = tag name (Name or ssh) and $2 is value to match
function ip_from_instance() {
  aws ec2 describe-instances \
    --filters "{\"Name\":\"tag:$1\", \"Values\":[\"$2\"]}" \
    --query='Reservations[0].Instances[0].PublicIpAddress' \
    | tr -d '"'
}

# ssh to aws host by Name tag: $1=username $2=hostname-tag
function ssh-aws-name() {
    ssh -i ${AWS_PEM} $1@$(ip_from_instance Name "$2")
}
```

## Scripts
Even functions can get rather unruly and one would need a script (or set of scripts) to accomplish an often repeated complex task. The script itself should consist of multiple functions except for simple, throw away scripts.

#### Scripts Directory
It is best to create a separate directory where user scripts are accumulated.  The `PATH` environment variable should then be set to point to the scripts directory.
```bash
$ mkdir ~/Scripts
```
Then add the following line to the `.bash_profile` or `.bashrc` file.
```bash
PATH="${PATH}:~/Sciripts"
```
After the above, any script file added to the `~/Scripts` directory can be executed from anywhere.

#### Creating Scripts
Scripts are just a text file that is executed in sequence as if each command was typed in at the command line prompt.  For example:
```bash
#!/bin/bash
# this file is: "~/Scripts/backup"
cp "$1" "$1".bak
```
To make the above script executable directly from anywhere, the following must hold true:
* The `~/Scripts` directory is added to `PATH` environment variable as shown in previous section.
* The script must start with the magic string `#!/bin/bash`.  This tells the Operating System that the file is to be executed as a `bash` script.
* The file must have execute permission.  This can be done as follows: `$ chmod +x ~/Scripts/backup`

The above script will create a backup of the given file name.  It can be used as follows:
```bash
// this will create a backup of foo.c as foo.c.bak
$ backup foo.c
```
