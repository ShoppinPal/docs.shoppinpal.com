# Setup a machine in the cloud

## Setup box on Azure

### Setup Dropbox on Azure

1. We can use dropbox for efficient 2-way project sync!
    * This approach works for any IDE - `atom` or `webstorm` or `vscode` - they don't have to know about the remote filesystem.
    * This will allow us to write code locally and have the changes show up on the remote box.
        * Adding/deleting files will work
        * File permissions will be properly reflected
        * Configuring `selective sync` via the dropbox UI will prevent the transfer of bulky dependencies back to your local filesystem
        * such features are often difficult to setup or absent in other sync tools.
    * Tools like `SourceTree` can simply deal with our local filesystem without any knowledge of the remote filesystem.
1. Install Dropbox agent
    * `sudo apt install nautilus-dropbox`
    * `echo "export LC_ALL=en_US.UTF-8 && export LANG=en_US.UTF-8" >> ~/.bashrc && source ~/.bashrc`
1. At this point you should **not** find any results when you run: `sudo find / -iname dropboxd`
1. Run `dropbox start -i` to install the daemon
1. It will get stuck because it's not showing you the logs which give the URL for linking your account
    ```
    $ dropbox status
    Starting...
    ```
1. Let's find the daemon:
    ```
    $ sudo find / -iname dropboxd
    /home/${USER}/.dropbox-dist/dropbox-lnx.x86_64-35.4.20/dropboxd
    /home/${USER}/.dropbox-dist/dropboxd
    ```
1. To stop the previous process we need its PID. The easiest way to find the PID is to run the same process again and it will tell you the PID of the process that's already running:
    ```
    # the path and file you found in the previous step
    $ /home/${USER}/.dropbox-dist/dropboxd
    Another instance of Dropbox (10537) is running!
    ```
1. Now kill it: `kill 10537` ... change `10537` to be the PID you see in your screen, ofcourse!
1  Now run it in foreground and you will get the account linking URL you need.
    1. copy/paste the url you see in the logs to your browser, follow the instructions
    1. you MUST NOT stop or kill the process while you are linking your account in the browser
    1. eventually the logs will give you a welcome message indicating that account linking its done
    ```
    $ /home/${USER}/.dropbox-dist/dropboxd
    ...
    Please visit https://www.dropbox.com/cli_link_nonce?nonce=secret to link this device.
    This computer isn't linked to any Dropbox account...
    Please visit https://www.dropbox.com/cli_link_nonce?nonce=secret to link this device.
    This computer is now linked to Dropbox. Welcome <user>
    ```
1. Now you should definitely use `ctrl+c` to stop the foreground process and check that a `Dropbox` folder exists: `ls -alrt ~/Dropbox`
1. Since the accounts are linked, start dropbox in background again: `dropbox start -i`
    1. NOTE: `dropboxd` will start syncing everything in your dropbox account immediately, the next few steps will work to correct this behaviour.
    1. But we want to tell `dropboxd` to avoid syncing anything other than our code/projects.
    1. Switch to your `Dropbox` directory and exclude any files that it has begun syncing: 
    ```
    cd ~/Dropbox/ && dropbox exclude add * && ls -alrt ~/Dropbox && dropbox status
    ```
1. Check the status: `dropbox status`
    1. If its still trying to sync then every few minutes, rerun: `cd ~/Dropbox/ && dropbox exclude add * && ls -alrt ~/Dropbox && dropbox status`
    1. After the status check declares: `Up to date`
        * Run this command one last time to be sure: `cd ~/Dropbox/ && dropbox exclude add *`
    1. Now the contents of your `Dropbox` directory should be empty: `cd ~/Dropbox/ && ls`
    1. Feel free to take a look at everything which has been excluded: `dropbox exclude list`
    1. If the directory you want to sync is also excluded, then remove it from exclude list by `~/bin/dropbox.py exclude remove [DIRECTORY] [DIRECTORY]`

### Maintainence

1. Uninstalling dropbox
    * `dropbox stop`
    * `sudo apt-get remove --purge nautilus-dropbox`
    * `sudo find / -iname dropboxd`
        * remove all the results, for ex: `rm -rf /home/${USER}/.dropbox-dist`
    * `sudo find / -iname dropbox`
        * `rm -rf /home/${USER}/Dropbox/.dropbox`
        * `rm -rf /home/${USER}/Dropbox/.dropbox.cache`
    * Unlink the machine from your dropbox account by finding its device name at: `https://www.dropbox.com/account/security` in the dropbox account online where it was previously linked and removing it. Otherwise you won't see the following logs to help you unlink from a previous account and relink to a new account if you are hoping to do an uninstall and then a reinstall eventually:
        ```
        This computer isn't linked to any Dropbox account...
        Please visit https://www.dropbox.com/cli_link_nonce?nonce=secret to link this device.
        ```
1. If you code using dropbox for sync long enough, you will run into an issue where dropbox will either crash or hang or both because of a limit on maximum number of files it can monitor for changes.
    * If you are lucky then the logs will magically pop-up on your console stating:

        ```
        Unable to monitor entire Dropbox folder hierarchy. Please run "echo fs.inotify.max_user_watches=100000 | sudo tee -a /etc/sysctl.conf; sudo sysctl -p" and restart Dropbox to fix the problem.
        Unable to monitor entire Dropbox folder hierarchy. Please run "echo fs.inotify.max_user_watches=100000 | sudo tee -a /etc/sysctl.conf; sudo sysctl -p" and restart Dropbox to fix the problem.
        ```
    * You can protect against this by [understanding](https://stackoverflow.com/questions/35711897/dropbox-fs-inotify-error) what is going on. For example I found out that I had provided significantly less resources than what dropbox recommends!

        ```
        # how many watchers have been made available?
        $ cat /proc/sys/fs/inotify/max_user_watches
        8192
        
        # how many watchers have been made available?
        $ sysctl fs.inotify.max_user_watches
        fs.inotify.max_user_watches = 8192
        ```
    * Or you could simply go ahead and make the fix:
        ```
        # 1. increase the number of watchers
        $ echo fs.inotify.max_user_watches=100000 | sudo tee -a /etc/sysctl.conf; sudo sysctl -p
        # 2. stop dropbox daemon if its running
        $ ~/bin/dropbox.py stop
        # 3. start the daemon again
        $ /opt/dropbox/dropboxd &

        # 4. check the status, it should start humming along again, soon:
        $ dropbox status
        Syncing (22,758 files remaining)
        Indexing 21,025 files...
        Uploading 1,729 files...
        
        $ dropbox status
        Syncing (21,995 files remaining)
        Indexing 19,825 files...
        Uploading 2,166 files...
        ```
    * You're welcome ;)

### Sync projects via Dropbox

1. Now that we've excluded everything known to us, you can place any new code-related projects & folders into dropbox and they will sync between.
    * https://www.digitalocean.com/community/questions/dropbox-works-with-digitalocean-droplets
        > You probably don't want to host content out of your Dropbox folder, but there's a basic trick for mirroring Dropbox content outside of the Dropbox folder: create a symbolic link.

        > Example: ln -s /var/www/foo.com ~/Dropbox/foo.com

        > This will cause Dropbox to treat /var/www/foo.com as if it resided inside the Dropbox folder. All other clients will see foo.com as a folder within the Dropbox folder, and will transparently sync across that symlink.

#### Other References
* https://www.digitalocean.com/community/tutorials/how-to-install-dropbox-client-as-a-service-on-ubuntu-14-04
* https://www.dropbox.com/install-linux
* https://github.com/jolantis/digitalocean-droplet-install-guide#setup-dropbox-sync
* http://www.dropboxwiki.com/tips-and-tricks/using-the-official-dropbox-command-line-interface-cli#EXCLUDE
* http://www.dropboxwiki.com/tips-and-tricks/install-dropbox-in-an-entirely-text-based-linux-environment#Post-installation
