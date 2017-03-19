# SFTP with Visual Studio (VSCode)

1. `Extensions: Install Extension`
1. Install `ftp-sync`
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