# SFTP with Visual Studio (VSCode)

1. `Extensions: Install Extension`
1. Install `ftp-sync`
    1. PROs:
        1. setup is simple via template file
    1. CONs:
        * syncing triggers are too involved
            * any file that you don't explicitly save doesn't get synced over
        * if you are coding for a long time, then even saving a file won't cause sync from `local to remote` to be triggered
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