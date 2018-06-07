# Setup Packer on Azure

```
sudo apt-get install unzip

cd ~/apps

wget https://releases.hashicorp.com/packer/1.2.4/packer_1.2.4_linux_amd64.zip

# On Unix systems, ~/packer or /usr/local/packer is generally good,
# depending on whether you want to restrict the install to just your user
# or install it system-wide. On Windows systems, you can put it wherever you'd like.

# it unzips the executable binary into the recommended folder for all users
sudo unzip packer_1.2.4_linux_amd64.zip -d /usr/local

# open the .bashrc file for editing
vi ~/.bashrc 

# add the following content in the file
export PATH=$PATH:/usr/local/packer

# refresh your shell
source ~/.bashrc 

# verify that the path has packer
echo $PATH

# you should see some output telling you how to use the command when you run
/usr/local/packer
```