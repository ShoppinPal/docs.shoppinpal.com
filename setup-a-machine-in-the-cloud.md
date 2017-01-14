## What is the problem?

I work remotely so when I was presented with an opportunity to travel and work side-by-side with my team, I was quite excited. But just a day before my travel plans, I received an update from `Docker for Mac beta` that made it impossible for me to download any container images due to some `ipv6` issues. After reaching my destination, the bandwidth became a challenge and I also learned that my immediate team found it extremely wasteful to use docker and docker-compose for the same reason. This coupled with the need for slightly more powerful machines \(bigger solid-state-drive `SSD`\), was why docker adoption across our company had been slow! We were well into adopting docker into staging and production but we would always trip over simple issues. It took days to get a solution from developer's environment to the staging environment.

## What is the solution?
We decided to resolve the bandwidth issue by hosting private machines in the cloud. Naturally, any container image downloads would be much faster for a machine sitting inside a datacenter. And the only stress on our bandwidth would be for the `ssh` session to the cloud-box which was minimal. Large and quickly scrolling logs could be problematic but they were manageable. Using solutions like `screen` or `mosh` further eased any concerns about `ssh` hang-ups which could kill our running containers.

![](/assets/box_in_cloud.jpeg)

## Challenges

Configuring the cloud-box per person was still a four hour activity! We cut this down to minutes with terraform scripting.

Some IDEs did a [poor job](../bug-in-webstorm-deployments.html) of syncing developer's local code to the cloud-box so we setup a recurring rsync which had a one-time setup cost.

## How was it received?
When we presented this solution to our developers who had struggled with adopting docker in the past, we received positive feedback. On our first day of adoption, we even discovered and resolved what would have become a `dev-to-staging` issue. It was bound to crop up late in the cycle and cause a crisis amongst developers and devops regarding product-readiness and now they found themselves working alongside to tackle issues quickly without any negative perceptions.

### Author TODOs:
- record a 5 min video where you get a digitalocean machine and set it up
- record a 2 min video where you use a script to set it up
- share the gist for the script for publication
etc.