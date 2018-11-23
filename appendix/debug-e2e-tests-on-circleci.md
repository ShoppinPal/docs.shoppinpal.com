# Debug e2e Tests on CircleCI

1. Click on "Rerun with SSH" on circle ci to rerun the build
2. Click on Enable SSH TAB
3. Inside that tab you will get "ssh_port" and "intance_ip"

Now, go to the terminal and SSH to the circleci Instance with following command

```text
ssh -p <ssh_port> <instance_ip> -L 5901:localhost:5900
```

Where,

**5901** is your localhost port mapped to the **5900** port of CircleCI instance

Now Open VNC client:
  - Type "Screen Sharing" in spotlight 
  - You will observe a popup asking for Hostname. Put below address 
  ```text localhost:5901 ``` and click connect
  Or, You can directly type "vnc://localhost:5901" in spotlight

upon asking for password enter `secret` as password.

Now manually run e2e test suite with base url http://localhost:3000 form the terminal 

and you will now be able to view the tests running in remote browser.

