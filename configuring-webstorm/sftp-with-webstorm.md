[](https://training.shoppinpal.com/setup.html)# Setup IDE

**Note**: _**This tutorial assumes you have already setup a droplet on DigitalOcean.**_

### Steps are documented below the video:

{% youtube %} https://www.youtube.com/watch?v=Ny02YT83ejY {% endyoutube %}

1. Open WebStorm
   1. Create New Project, or
   1. Open an existing one.
1. Goto **Tools &gt; Deployment &gt; Configuration**

   This will open the configuration window where you will be adding a server .

1. Click on "**+**" Symbol i.e.** Add Deployment Server**

1. Now In** Connection tab**, specify the name you want to give to this deployment server. For eg. **Webstorm Remote Access**

1. Now Select Type i.e. FTP, SFTP, FTPS or Local . Here we are describing the** interaction type **with the remote host.

   1. **FTP** : File Transfer Protocol

   2. **SFTP**: SSH File Transfer Protocol

   3. **FTPS**: FTP-SSL \(extension to FTP\)

   4. **Local**

1. For This demo,** We will be selecting SFTP**.

1. Now Specify other details as :

   1. **Host** : mention the IPv4 address of your droplet.
   1. **port** : 22
   1. **rootpath**: / \(Specifies the root path of your droplet. Leave it alone if you are not an advanced user\)
   1. **username**: username for logging into your droplet. For digitalocean droplets, it will usually be `root`
   1. **Auth type**: Change it from `Password` to `Key pair`
      1. **Private key file**: You can use the `...` symbol to enter the file browser and 9 times out of 10, the file you want to select is located here: `/Users/<your_username>/.ssh/id_rsa` on a mac.
      1. **Key passphrase**: Provide the password you used to encrypt your `id_rsa` file.
         1. enable the `Save passphrase` checkbox
1. Additionally click on "**Test SFTP Connection**" to verify if your connection is authorized or not.
1. Once your connection is successful, navigate to** Mappings tab **.
   1. **Local Path** : path of your application in your system
   11. **Deployment Path** : path of your application on the remote host. For eg. /root/dev/BluBox where BluBox is the application directory.
1. For advanced users:
   * You can chose to ignore few directories which we want i.e. `node modules`, `bower_components` etc. by adding them to excluded paths.
1. Now Click on **OK**.
1. Your Webstorm Deployment Server Configuration is complete.
   1. If you used an **existing project**:
      1. Click on **Tools &gt; Deployment**  and select **Sync with Deployed to Webstorm Remote Access.**
         1. It will take some time to sync local project with the remote one.
1. Goto **Tools &gt; Deployment** menu and select **Automatic Upload**
1. Now whenever you save changes, **the code is uploaded on the remote host**
   * Advanced users: Additionally if your remote box is configured appropriately, then your application is re-deployed with the updated code. But that's a separate topic.
