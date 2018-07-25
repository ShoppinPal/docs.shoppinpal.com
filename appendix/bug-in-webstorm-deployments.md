# Bug in WebStorm deployments

File Permissions from the local file system are not synced properly to the remote box when using SFTP with WebStorm. Webstorm calls this process `Deployment`.

For example, if you had a script that could be executed because its permissions were set to `744` or `+x` on your local box, it will not work on the remote box as the permissions will not match.

