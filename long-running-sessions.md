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
* How do I kill a `screen` session?
    * `screen -X -S SESSION_ID quit`
* How do I kill my current `screen` session?
    ```
    screen -X -S `echo -n $STY` quit
    ```
* How do I [scroll](http://serverfault.com/questions/206303/how-to-scroll-back-in-screen-within-a-ssh-session-from-os-x)?
    * Inside the `screen` session you can use: `CTRL+A (release), [`
        * You can then use the arrows to scroll around the window. To get out of scrolling you can use `CTRL+C`
    * `Ctrl + A, ESC` and then vim-like commands: `Ctrl + u or Ctrl + d`
    * You can [modify](http://slaptijack.com/system-administration/mac-os-x-terminal-and-gnu-screen-scrollback/) `.screenrc` to allow mouse-based scrollback.
        ```
        # added on july 19 2017 by pulkit
        # after editing the source from: https://gist.github.com/ChrisWills/1337178
        
        # GNU Screen - main configuration file
        # All other .screenrc files will source this file to inherit settings.
        # Author: Christian Wills - cwills.sys@gmail.com
        
        # Allow bold colors - necessary for some reason
        attrcolor b ".I"
        
        # Tell screen how to set colors. AB = background, AF=foreground
        termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'
        
        # Enables use of shift-PgUp and shift-PgDn
        termcapinfo xterm|xterms|xs|rxvt ti@:te@
        
        # Erase background with current bg color
        defbce "on"
        
        # Enable 256 color term
        term xterm-256color
        
        # Cache 999999 lines for scroll back
        defscrollback 999999
        
        hardstatus alwayslastline
        
        # Very nice tabbed colored hardstatus line
        hardstatus string '%{= Kd} %{= Kd}%-w%{= Kr}[%{= KW}%n %t%{= Kr}]%{= Kd}%+w %-= %{KG} %H%{KW}|%{KY}%101`%{KW}|%D %M %d %Y%{= Kc} %C%A%{-}'
        
        # Hide hardstatus: ctrl-a f
        bind f eval "hardstatus ignore"
        
        # Show hardstatus: ctrl-a F
        bind F eval "hardstatus alwayslastline"
        ```

