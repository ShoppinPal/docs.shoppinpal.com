# SFTP with WebStorm

**Note**: _**This tutorial assumes you have already**_ [_**setup a droplet on DigitalOcean.**_](https://training.shoppinpal.com/setup.html)

## Steps are documented below the video:

{% embed data="{\"url\":\"https://www.youtube.com/watch?v=Ny02YT83ejY\",\"type\":\"video\",\"title\":\"\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/Ny02YT83ejY/maxresdefault.jpg\",\"width\":1280,\"height\":720,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/Ny02YT83ejY?rel=0&showinfo=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/Ny02YT83ejY?rel=0&amp;showinfo=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}

1. Open WebStorm
   1. Create New Project, or
   2. Open an existing one.
2. Goto **Tools &gt; Deployment &gt; Configuration**

   This will open the configuration window where you will be adding a server .

3. Click on "**+**" Symbol i.e. **Add Deployment Server**
4. Now In **Connection tab**, specify the name you want to give to this deployment server. For eg. **Webstorm Remote Access**
5. Now Select Type i.e. FTP, SFTP, FTPS or Local . Here we are describing the **interaction type** with the remote host.
   1. **FTP** : File Transfer Protocol
   2. **SFTP**: SSH File Transfer Protocol
   3. **FTPS**: FTP-SSL \(extension to FTP\)
   4. **Local**
6. For This demo, **We will be selecting SFTP**.
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
9. Once your connection is successful, navigate to **Mappings tab** .
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

