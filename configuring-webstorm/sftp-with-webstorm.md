# Setup IDE

**Note**: _**This tutorial assumes you have already setup a droplet on DigitalOcean.**_

### Steps are documented below the video:

{% video %}

https://www.dropbox.com/s/8bfswltk47f5sfz/Webstorm%20Configuration%20For%20Code%20Deployment%20on%20Remote%20Host%20.mp4?dl=0

{% endvideo %}

1. Open WebStorm
   1. Create New Project, or
   2. Open an existing one.
2. Goto **Tools &gt; Deployment &gt; Configuration**

   This will open the configuration window where you will be adding a server .

3. Click on "**+**" Symbol i.e.** Add Deployment Server**

4. Now In** Connection tab**, specify the name you want to give to this deployment server. For eg. **Webstorm Remote Access**

5. Now Select Type i.e. FTP, SFTP, FTPS or Local . Here we are describing the** interaction type **with the remote host.

   1. **FTP** : File Transfer Protocol

   2. **SFTP**: SSH File Transfer Protocol

   3. **FTPS**: FTP-SSL \(extension to FTP\)

   4. **Local**

6. For This demo,** We will be selecting SFTP**.

7. Now Specify other details as :

   1. **Host** : mention the IPv4 address of your droplet.
   2. **port** : 22
   3. **rootpath**: / \(Specifies the root path of your droplet. Leave it alone if you are not an advanced user\)
   4. **username**: username for logging into your droplet. For digitalocean droplets, it will usually be `root`
   5. **Auth type**: Change it from `Password` to `Key pair`
      1. **Private key file**: You can use the `...` symbol to enter the file browser and 9 times out of 10, the file you want to select is located here: `/Users/<your_username>/.ssh/id_rsa` on a mac.
      2. **Key passphrase**: Provide the password you used to encrypt your `id_rsa` file.
         1. enable the `Save passphrase` checkbox

8. Additionally click on "**Test SFTP Connection**" to verify if your connection is authorized or not.

9. Once your connection is successful, navigate to** Mappings tab **.  
   1. **Local Path** : path of your application in your system  
   2. **Deployment Path** : path of your application on the remote host. For eg. /root/dev/BluBox where BluBox is the application directory.

10. For advanced users:

    * You can chose to ignore few directories which we want i.e. `node modules`, `bower_components` etc. by adding them to excluded paths.

11. Now Click on **OK**.
12. Your Webstorm Deployment Server Configuration is complete.
    1. If you used an **existing project**:
       1. Click on **Tools &gt; Deployment**  and select **Sync with Deployed to Webstorm Remote Access.**
          1. It will take some time to sync local project with the remote one.
13. Goto **Tools &gt; Deployment** menu and select **Automatic Upload**
14. Now whenever you save changes, **the code is uploaded on the remote host**
    * Advanced users: Additionally if your remote box is configured appropriately, then your application is re-deployed with the updated code. But that's a separate topic.



