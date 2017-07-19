# Setup a machine in the cloud

## Setup box

### Long Running Sessions

Using solutions like `screen` or `mosh` can help workaround `ssh` hang-ups which can kill any child processes of an active ssh session.

#### Screen

* How do I start `screen`, during an active `ssh` session?
    * `screen`
        * will start a screen session with a random name
* How do I list any pre-existing `screen` sessions?
    * `screen -ls`
* How do I rename a pre-existing `screen` session?
    * `screen -S old_session_name -X sessionname new_session_name`
* How to [check](https://serverfault.com/questions/257975/how-to-check-if-im-in-screen-session) if I'm in a `screen` session?
    * `echo $STY`
        * If you are inside a screen session, the output will be the session name
        * otherwise, the output will be empty
* How do I find my current `screen` session's name?
    * `echo $STY`
* How do I [scroll](http://serverfault.com/questions/206303/how-to-scroll-back-in-screen-within-a-ssh-session-from-os-x)?
    * Inside the `screen` session you can use: `CTRL+A (release), [`
        * You can then use the arrows to scroll around the window. To get out of scrolling you can use `CTRL+C`
    * `Ctrl + A, ESC` and then vim-like commands: `Ctrl + u or Ctrl + d`
    * You can [modify](http://slaptijack.com/system-administration/mac-os-x-terminal-and-gnu-screen-scrollback/) `.screenrc` to allow mouse-based scrollback.

