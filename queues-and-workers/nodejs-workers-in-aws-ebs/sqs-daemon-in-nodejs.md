# Queues & Workers

## NodeJS workers in AWS EBS

### SQS Daemon in NodeJS

1. Does not work well when there are more messages than workers.
    * It either does not know: `How to wait for success on current request to workers before sending more messages to workers for processing`
    * or we did not know how to properly configure it!
1. _to be determined..._