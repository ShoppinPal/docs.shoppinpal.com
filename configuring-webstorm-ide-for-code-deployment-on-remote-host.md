## Configuring Webstorm IDE For Code Deployment on Remote Host

![](/assets/WebStorm.jpg)

We are continuously looking for improving our developers life by discovering new techniques which allow them to work in their most productive way. Today, we will be looking at similar tool which allow developers to directly verify their changes on the server without worrying about version control terminologies like committing the code, pushing it in the git repository.

The Idea here is simple, We will configure Webstorm IDE such that whenever developers save the code in IDE, it will directly upload the updated code in the remote host working directory.

In Short, _**Webstorm will be continuously syncing local code with the code on remote host**._

For this We will be using _**SFTP functionality in Webstorm IDE**_, So Lets Get Started :

#### **Note**: _**This tutorial assumes you have already setup a droplet on DigitalOcean.**_

### Steps are documented below the video:

1. .Open **Webstorm IDE &gt; Tools &gt; Deployment &gt; Configuration**

   This will open the configuration window where you will be adding a server .

2. Click on "**+**" Symbol i.e.** Add Deployment Server**

3. Now In** Connection tab** ,Specify The Name You want to give to this deployment server. For eg. **Webstorm Remote Access**

4. Now Select Type i.e. FTP, SFTP, FTPS or Local . Here we are describing the** interaction type **with the remote host.

   1. **FTP** : File Transfer Protocol

   2. **SFTP**: SSH File Transfer Protocol

   3. **FTPS**: FTP-SSL \(extension to FTP\)

   4. **Local**

5. For This demo,** We will be selecting SFTP**.

6. Now Specify other details as :

   1. **Host** : mention the IPv4 address of your droplet.

   2. **port** : 22

   3. **rootpath**: / \(this specifies root path of your droplet\)

   4. **username**:username for loggin into your droplet. For eg. root

   5. **password**: your password

7. Additionally click on "**Test SFTP Connection**" to verify if your connection is authorized or not.

8. Once your connection is successful,Navigate to** Mappings tab **.

   1. **Local Path** : path of your application in your system

   2. **Deployment Path** : path of your application on the remote host. For eg. /root/dev/BluBox where BluBox is the application directory.

9. Additionally we can chose to ignore few directories which we want i.e.node modules\_,\_bower\_components etc. by adding them to excluded paths.

10. Now Click on **OK**.

11. Your Webstorm Deployment Server Configuration is complete.

12. Now Click on **Tools &gt; Deployment**  and select **Sync with Deployed to Webstorm Remote Access.**

13. It will take some time to sync local project with the remote one.

14. after synchronization, select **automatic upload** from **tools &gt; deployment** menu.

15. Now whenever you save changes, **the code is uploaded on the remote host and application is re-deployed with the updated code.**



