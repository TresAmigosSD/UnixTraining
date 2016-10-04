# Use TMUX

Tmux is an enhanced version of the old "screen" tool. It is very useful when working on remote servers.
The most useful function for us is the "detach-attach" function. Here is a simplest use case:
* `$ tmux`  (start a new tmux session)
* do your work as usual for the day
* When you finish the day and prepare to go home, hit `Ctrl-b` and then `d` (detach from current tmux session)
* Now your in the normal shell again, you can "exit" or just do `Ctrl-d` to logout from the server
* Disconnect and go home
* Come in the next morning, ssh to server
* `$ tmux a` (attach to last active session)
* Now you get back to whatever you left the day before

The biggest advantage of using Tmux is that you can "detach" while the work is running. For example, you are  running an `SmvModule`, which takes very long time. You don't need to wait for it to finish to go home, instead you just need to "detach" the Tmux session and go home, and attach it next morning.
There are other benefit of Tmux, such as multiple windows and panels. Please Google and learn those if you want to make better use of it.

## Pass down Shell environment to Tmux sessions
Since the Shells run in the Tmux are alive even you get disconnected, when your login shell's environment variable get updated the shells in Tmux will not get updated automatically. Each server could have different environment variables, which changes from login to login, need to figure them out each time your are using a different server. The following are 2 example functions, which I used in one server in my ".bashrc" file.

```shell
function tmuxa() {
    cat << EOF > ${HOME}/.tmux_env
    export SSH_AGENT_PID=$SSH_AGENT_PID
    export SSH_AUTH_SOCK=$SSH_AUTH_SOCK
    export DA_SESSION_ID_AUTH=$DA_SESSION_ID_AUTH
    export KRB5CCNAME=$KRB5CCNAME
    export CDC_JOINED_DC=$CDC_JOINED_DC
EOF
    tmux a $@
}

function tmuxenv() {
  source ${HOME}/.tmux_env
}
```

With those functions, from the login shell, instead of type "tmux a" to re-attach to existing tmux session, I just use `tmuxa` command, and then within the shells in the Tmux session I just type "tmuxenv" to update the environment variables.

## Tmux shortcuts

|Task|shortcuts|
|:---|:---|
| attach to session named RNN| tmux a -t RNN|
| list session names| tmux ls|
| start new session myname| tmux new -s myname|
| rename session | tmux rename-session -t old_name new_name   (if old_name is not entered, it will * rename the recently used session)|
| kill session | tmux kill-session -t myname|
| panes split | horizontal split `ctrl+b  "` vertical split `ctrl+b  %`|

With the `tmuxa` function defined in the `.bashrc`, to attach to a session with name `RNN` should be
```
tmuxa -t RNN
```

## Use mouse in Tmux
Please refer http://www.davidverhasselt.com/enable-mouse-support-in-tmux-on-os-x/ for how to setup Tmux so that you can use mouse to select windows change window size, etc

Basically add the following lines to `~/.tmux.conf`
```
set -g mode-mouse on
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mouse-select-window on
```
With that configuration, terminal on screen mouse selection may need to press the "option/alt" key on the keyboard.
