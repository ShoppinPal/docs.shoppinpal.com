# Setup a machine in the cloud

## Remaining Challenges

Configuring the cloud-box per person is still a manual activity! We hope to cut this down to minutes with `terraform` scripting one day.

Some IDEs do a [poor job](../bug-in-webstorm-deployments.html) of syncing developer's local code to the cloud-box so we setup a recurring rsync which had a one-time setup cost.

## How was it received?

When we presented this solution to our developers who had struggled with adopting docker in the past, we received positive feedback. On our first day of adoption, we even discovered and resolved what would have become a `dev-to-staging` issue. It was bound to crop up late in the cycle and cause a crisis amongst developers and devops regarding product-readiness and now they found themselves working alongside to tackle issues quickly without any negative perceptions.
