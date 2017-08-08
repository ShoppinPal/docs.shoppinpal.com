# NodeJS Profiling

## Best NodeJS Versions for profiling 
If possible, do yourself a favor and test your code to make sure it works with NodeJS version 6.3 or greater.
    * Official [support](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27) for Node.js debuggability landed in Node.js version 6.3 in May 2016.
    * Before v6.3: https://github.com/node-inspector/node-inspector
    
## Profiling

### Memory

1. expose port 9229 and start your `web` service
    ```
    dc up -d web && \
        dc logs --follow --timestamps web
    ```
2. connect with `chrome://inspect/#devices`
3. take a snapshot
4. run requests against web server or your one-time nodejs code
5. took another snapshot