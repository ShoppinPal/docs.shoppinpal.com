# Queues & Workers

## PHP

![](/assets/Worker architecture.png)

1. `messages` are sent to SQS.
2. A static amount (configurable) of PHP `workers` are kept alive by the `Supervisor`.
    * Given the nature of PHP, we optimize `workers` to stop and restart every X minutes.
3. While workers are running, they attempt to fetch messages from SQS.
    * If a `worker` gets a `message` then it starts working on that job and takes it to completion.
    * If a `worker` crashes while processing then the `Supervisor` will bring it back up.
        * What will happen to the message that was pulled off the queue by that "crashed" `worker`?
        * Will the resurrected worker start work on the same exact `message` again?

![](/assets/Worker timeline.png)
