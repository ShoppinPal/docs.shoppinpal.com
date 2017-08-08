## How to find Node.js Performance optimization killers

As we all Know , Node.js is based on [V8 Javascript Engine](https://github.com/v8/v8/wiki). in Node.js, _the code is optimized dynamically; this means that the code is optimized according to its runtime behavior._

After reading this post, you should be able to:

1. Detect if the function is optimized by the JavaScript Engine\(V8\).
2. Detect if an optimized function is de-optimized \(this can happen as optimization is done dynamically\).
3. Detect why a function cannot be optimized.

this article aims to make those methods available for most Node.js developers so they can be more productive when it comes to optimizing their node.js apps.

### Brief Overview of Node.js Performance Optimization in V8 Javascript Engine

Though currently lots of efforts are being taken to make node.js independent from V8 Engine,most node.js apps are based on V8 javascript engine.we will understanding the optimization process for V8 engine in this article.

> In V8, the code is optimized dynamically; this means that the code is optimized according to its runtime behavior.

The process occurs during runtime. V8 analyzes the behavior of the code, develops heuristics and proceeds to optimizations based on what it observed.

For instance, V8 spies on the inputs and the outputs of the functions in order to see if it can perform type assertions. If the type of the arguments of a function is always the same, it seems safe to optimize this function from this assertion.

V8 performs diverse cases of optimization, but the one based on the argument's type is probably the easiest to describe.

### How Optimization is done.....

```
// index.js

function myFunc(nb) {  
    return nb + nb;
}

for (let i = 0; i < 2000; ++i) {  
    myFunc(i);
}
```

Usually, to run this file, we would use the command

`$ node index.js`

To trace optimizations, we will add an argument to the command line.

```
$ node --trace-opt index.js | grep myFunc
```

the result appears to be ,

```
[marking 0x2bc3091e7fc9 
<JS Function myFunc (SharedFunctionInfo 0x1866a5c5eeb1)> 
for recompilation, reason: small function, ICs with typeinfo: 1/1 (100%), generic ICs: 0/1 (0%)]
[compiling method 0x2bc3091e7fc9 
<JS Function myFunc (SharedFunctionInfo 0x1866a5c5eeb1)> 
using Crankshaft]
[optimizing 0x2bc3091e7fc9 
<JS Function myFunc (SharedFunctionInfo 0x1866a5c5eeb1)> 
- took 0.009, 0.068, 0.036 ms]
[completed optimizing 0x2bc3091e7fc9 
<JS Function myFunc (SharedFunctionInfo 0x1866a5c5eeb1)>
]
```

The function was marked for recompilation. That is the first step of the optimization of a function.

The function has then been recompiled and optimized.

### ... followed by a de-optimization {#followedbyadeoptimization}

```
// index.js

function myFunc(nb) {  
    return nb + nb;
}

for (let i = 0; i < 2000; ++i) {  
    myFunc(i);
}

for (let i = 0; i < 2000; ++i) {  
    myFunc(i + '');
}
```

The code is pretty much the same here. But this time, after calling the function with numbers only, we call it with a few strings. It is still a perfectly valid code since the`+ `operator can be used for number addition and string concatenation.Now running bellow command 

```
node --trace-deopt --trace-opt index.js | grep myFunc
```

gives us,

```
[marking 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)> for recompilation, reason: small function, ICs with typeinfo: 1/1 (100%), generic ICs: 0/1 (0%)]
[compiling method 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)> using Crankshaft]
[optimizing 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)> - took 0.010, 0.076, 0.021 ms]
[completed optimizing 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)>]
[deoptimizing (DEOPT eager): begin 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)> (opt #0) @1, FP to SP delta: 24, caller sp: 0x7ffe2cde6f40]
  reading input frame myFunc => node=4, args=2, height=1; inputs:
      0: 0xc6b3e5e7fb9 ; [fp - 16] 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)>
  translating frame myFunc => node=4, height=0
    0x7ffe2cde6f10: [top + 0] <- 0xc6b3e5e7fb9 ;  function    0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)>  (input #0)
[deoptimizing (eager): end 0xc6b3e5e7fb9 <JS Function myFunc (SharedFunctionInfo 0x87d8115eec1)> @1 => node=4, pc=0x30c7754496c6, caller sp=0x7ffe2cde6f40, state=NO_REGISTERS, took 0.047 ms]
[removing optimized code for: myFunc]
[evicting entry from optimizing code map (notify deoptimized) for 0x87d8115eec1 <SharedFunctionInfo myFunc>]
```

The first part of this log is pretty similar to the previous paragraph.

However, there is a second part in which the function is de-optimized: V8 detected that the type assumption made before \(“inputs of myFunc are numbers”\) was false.

> **Even if JavaScript is not strongly typed, V8 has optimization rules which are. Therefore, it is a good idea to have coherent typings as arguments and return values of a function.**

but there are patterns in JavaScript that can have very different behaviors at runtime. V8 decides to never optimize those functions to avoid to fall in a **de-optimization hell.**

### De-optimization hell {#deoptimizationhell}

De-optimization hell happens in V8 when a function is optimized and de-optimized a lot during the runtime.

After a few cycles optimization/de-optimization, V8 will flag the method as not optimizable. However, a significant amount of time will have been lost in this cycle with impact on the process performances and memory consumption.

## Conclusion {#conclusion}

> In this article, we saw how to trace optimizations, de-optimizations, and non-optimizations in Node.js. This is a good starting point for your journey through optimizing your Node.js code.

A high-level tool to explore optimization and de-optimization is named [IRHydra](http://mrale.ph/irhydra/2/). A short introduction to its usage with Node.js can be found on [Eugene Obrezkov’s blog](https://blog.ghaiklor.com/tracing-de-optimizations-in-nodejs-2ba16900fc6f#.p06hncpvs).



