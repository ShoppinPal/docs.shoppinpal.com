# NodeJS Profiling

## Best NodeJS Versions for profiling

If possible, do yourself a favor and test your code to make sure it works with NodeJS version 6.3 or greater.

* Official [support](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27) for Node.js debuggability landed in Node.js version 6.3 in May 2016.
* Before v6.3: [https://github.com/node-inspector/node-inspector](https://github.com/node-inspector/node-inspector)

## Profiling

### Memory

1. expose port 9229 if using docker
2. and start your code: `node --inspect --debug-brk myCode.js`
   1. it will output a url to connect with `chrome://inspect/#devices`, go ahead and copy/paste that URL into chrome
3. under the `sources`tab, place breakpoints where ever you want ... then hit play to let the code run
   * Your code starts in "paused" mode because of `--debug-brk`
4. take a snapshot, then:
   1. either, run requests against web server to cause load
   2. or, simply let your one-time nodejs code run until it hits a breakpoint
5. take another snapshot
6. compare heap snapshots in chrome devtools

