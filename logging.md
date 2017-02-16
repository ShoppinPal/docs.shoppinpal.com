# Logging

## Key Lessons

1. Always log to stdout. It is not the application's responsibility to route logs.
2. Never, ever log credentials, passwords or any sensitive information.

## Resources

1. https://blog.risingstack.com/node-js-logging-tutorial/
2. https://www.loggly.com/blog/three-node-js-libraries-which-make-sophisticated-logging-simpler/

## Worth Exploring

1. [LogTown](https://github.com/logtown/logtown) - You can use any logger you want underneath it.

## Notes from Folks

### By [Pulkit Singhal](https://github.com/pulkitsinghal):
> I think I was able to crystallize what was bothering me about the state of logging in nodejs. Here are some high level use cases I'd like to see all mashed up and addressed by one library:
1. Turning off logging in modules for tests like mocha (doable with env flag and any log library)
2. Toggling logs in dependencies when troubleshooting (again nothing special if the dependency has env flag)
3. Low level information like line numbers (tracer provides this)
4. Log levels (bunyan/winston provide this but debug doesn't)
5. Namespace based toggling for logs (bunyan/winston miss this while debug provides it)
6. Human readable json print out to console AND files. Winston doesn't prettyPrint to log files and even what it does print is such a far cry from how it would look compared to console.log that without custom formatting I can't see how to use it. For example logging an array looks quite different, it almost made me think I had the wrong data structure the first time around.

> I feel like there is some room for improvement. I would love to see debug and tracer mashed together somehow ... found debug-trace interestingly enough ... with the added capability to log to files and have log levels.