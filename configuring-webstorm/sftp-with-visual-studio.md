# SFTP with Visual Studio (VSCode)

1. `Extensions: Install Extension`
1. Install `ftp-sync`
    * PROs:
        * setup is simple via template file
    * CONs:
        * syncing triggers are too involved
        * any file that you don't explicitly save, will not be synced over
        * if you are working for a long time without sync  then even saving a file won't cause the trigger from `local to remote` to activate
        * file permissions aren't synced over from local to remote accurately
        * no clear way to setup 2-way automatic sync

1. Configure the generated template file `myProject/.vscode/ftp-sync.json`:
    ```
{
    "remotePath": "/root/dev/myProject",
    "host": "my-digitalocean-box.domain.com",
    "username": "root",
    "port": 22,
    "secure": true,
    "protocol": "sftp",
    "uploadOnSave": true,
    "passive": false,
    "debug": false,
    "privateKeyPath": "/path/to/.ssh/id_rsa",
    "passphrase": "password_for_id_rsa",
    "ignore": [
        "\\.vscode",
        "\\.git",
        "\\.DS_Store"
    ]
}
    ```
1. That's it.