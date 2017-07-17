# Setup a machine in the cloud

## Setup box

### Shared FileSystem

Instead of setting up various plugins across IDEs for remote editing projects, it may be better to spend that time setting up some sort of shared filesystem via IDE-agnostic technologies such as `rsync` or `sshfs`


#### sshfs

1. Install osxfuse on mac: https://github.com/osxfuse/osxfuse/releases/tag/osxfuse-3.6.2
1. Install sshfs on mac: https://github.com/osxfuse/sshfs/releases/tag/osxfuse-sshfs-2.5.0
1. Follow along: https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh
