# Setup a machine in the cloud

## What is the solution?

We decided to resolve the bandwidth issue by hosting private machines in the cloud. Naturally, any container image downloads would be much faster for a machine sitting inside a datacenter. And the only stress on our bandwidth would be for the `ssh` session to the cloud-box which was minimal. Large and quickly scrolling logs could be problematic but they were manageable. Using solutions like `screen` or `mosh` further eased any concerns about `ssh` hang-ups which could kill our running containers.

![](/assets/box_in_cloud_3.jpeg)
