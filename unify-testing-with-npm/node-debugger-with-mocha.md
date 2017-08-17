# Using Node Debugger with Mocha

## Assumption
With a package.json that has the following lines:
```
scripts: {
    "mocha": "mocha"
}
```

## Steps
* nodejs `v6.3.0` and mocha `v3.1.0`
    * you can use V8 inspector integration
    * `--inspect` activates V8 inspector integration
    * `--debug-brk` adds a breakpoint at the beginning
    * You can run: `npm run mocha -- --inspect --debug-brk`
* nodejs `v7.6.0` and mocha `v3.3.0`
    * You can run: `npm run mocha -- --inspect-brk`
        * `--inspect-brk` is a shorthand for --inspect --debug-brk

# References

* [https://stackoverflow.com/questions/14352608/whats-the-right-way-to-enable-the-node-debugger-with-mochas-debug-brk-switch\#answer-39901169](https://stackoverflow.com/questions/14352608/whats-the-right-way-to-enable-the-node-debugger-with-mochas-debug-brk-switch#answer-39901169)



