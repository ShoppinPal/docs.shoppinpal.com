# Promises

## What are promises

The absolute reference: https://www.promisejs.org/

![](/assets/Screen Shot 2017-02-02 at 4.15.35 AM.png)

1. Promises are nothing but a chain of success/fail events
2. We can use promises in nested callback  which are dependent to each other this is termed as a callback hell It is hard to understand and creates lot of confusion.
3. Promises can handle global errors.
4. Promises can be chained (you don't have this encapsulation like callbacks)
5. Promise is an interface class that helps you to control if the call to a function - that may be executed asynchronously - has finished successfully or with an error. It is very similar to have a try-catch-finally block for async calls.

## What are some implementations

1. Bluebird
2. Q

## What should we use

1. Bluebird is the best
2. Sadly angular uses a subset of Q which is packaged as $q
that is sad
3. but we do have options like replacing it with a bluebird based promise library that you can use
    * https://github.com/mattlewis92/angular-bluebird-promises
    * Replaces the default angular $q service with the bluebird promise library for enhanced promises within your angular app!