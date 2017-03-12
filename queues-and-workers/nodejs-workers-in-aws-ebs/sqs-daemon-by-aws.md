# Queues & Workers

## NodeJS workers in AWS EBS

### SQS Daemon by AWS

1. `nginx` sits between `sqsd` and workers for no good reason!
    * Its presence creates more issues:
        * `5xx` errors that claim "loss of connection to upstream server"
        * connection errors like `ECONNRESET` and various other socket hangup problems
1. `sqsd` itself is quite buggy too
    * messages end up on dead letter queue (`DLQ`) despite the worker reporting `200 OK` for success.