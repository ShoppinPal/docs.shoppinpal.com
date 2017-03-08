# Queues & Workers

A Queue+Worker infrastructure is meant:
- to run asynchronous jobs,
- scale up & down easily.


A `message` contains the data required to run a job.
A `Queue` is where the messages are posted, its like a job board.
A `Worker` performs all the heavy lifting and finishes the job based on the `message`.

