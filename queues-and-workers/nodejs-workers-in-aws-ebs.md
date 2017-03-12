# Queues & Workers

## NodeJS workers in AWS EBS

We tested NodeJS workers in AWS EBS using slightly different architectures:

1. with `sqsd` provided out-of-the-box (OOTB) in an AWS VM which would pull from SQS and hand a message to our worker.
2. with a nodejs [sqsd](https://www.npmjs.com/package/sqsd) standalone component which would pull from SQS and hand a message to our worker.
3. with our worker pulling a message directly from SQS itself.
    * This is similar to the architecture described for [PHP workers in AWS EBS](/queues-and-workers/php-workers-in-aws-ebs.md) with one important distinction, the `supervisor` isn't involved.
