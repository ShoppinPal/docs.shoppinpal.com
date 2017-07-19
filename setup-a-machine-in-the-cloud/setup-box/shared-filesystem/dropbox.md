# Setup a machine in the cloud

## Setup box

### Shared FileSystem

#### Dropbox

1. Install Dropbox agent
    * https://www.dropbox.com/install-linux
    * for digitalocean 64-bit droplets with Ubuntu OS:

    ```
    cd ~ && \
    wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf - && \
    ~/.dropbox-dist/dropboxd
    ```
1. Link the machine by copy/pasting the URL from the output window into your browser. Here's a sample of what you'll see:

        ```
    This client is not linked to any account...
    Please visit https://www.dropbox.com/cli_link?host_id=xxx
    to link this machine.
    ```
1. Use `ctrl+c` to terminate the `dropboxd` process otherwise it will start syncing everything in your dropbox account immediately, which will create problems if your remote machine doesn't have enough space!
1. 