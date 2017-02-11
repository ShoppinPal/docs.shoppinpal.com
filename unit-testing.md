# Unit Testing for Angular \(karma + jasmin\)

TDD is an essential part of any software development cycle. Here's a story from my past which relates its importance:
> I created a filter module for products just like amazon or flipkart have. I tested it well on my machine and it was working great. Then came the day of live demo to our client, where this filter suddenly stopped working! It was doing nothing in our staging env and it was kind of embarrassing.

The next day, I decided to create unit tests for each every function that I wrote. As developer we should feel confident in our code's ability to run well, therefore, we must learn to love the feeling of having a watertight app that comes with automated testing.

Apart from my stories let us start a real example. You can follow [AngularUnitTestDemo](https://github.com/Mohammed-Aadil/AngularUnitTestDemo) on github or clone a local copy to begin with.

## Motivation behind this blog

This blog contains fundamentals of angular unit testing that we are using in [Shoppinpal](https://www.shoppinpal.com). It is a beginner's guide on unit testing for Developers and QA engineers. At the end of this blog, you should have sufficient knowledge for creating simple unit tests in AngularJS.

## How to write the test

Everyone has the same question when writing tests for first time.
- You must break down the logic of your application into small chunks or units and verify that each chunk works perfectly and as desired.
- **In javascript the smallest individual chunk you can test is usually functions. The core feature in application must be verified with accompanying unit tests.**
- Unit testing must be done on the basis of input and output for an individual function so when functions are joined together, your code has a better chance to work as a whole.
- It is better not to interfere with the operation of a function.

Best practice says you should write your unit test before actual development starts. You must be questioning yourself, how can we possibly do that? The answer is simple: just create an empty unit test for the function, keep updating it when function is updated, and freeze it when final touches are made on that function's development. Now if any newcomers try to make changes in code, they would easily find out about any mistakes if & when the tests break.

Unit tests must be broken down into 3 parts:

1. Story
2. Feature
3. Units

So in our case Story is \`_Users come to our page and login, if successful they are redirected to Profile page_\`. In this we state that our feature is user login and we further divide this feature into units as follows:

1. Ensure invalid emails do not pass.
2. Ensure valid emails pass the validation.
3. Ensure path changes on user logged in.

```
describe("user login form", function() {
    it("Ensure invalid emails do not pass", function() {});
    it("Ensure valid emails pass the validation", function() {});
    it("Ensure path changes on user logged in", function() {});
});
```

## Configuring karma + jasmin for our angular app

### Introduction to tools

**Karma** is a test runner and it is a direct product from angularJS team. It provides flexibility to test your app in various browsers and is integrated with Jenkins, TravisCI and CircleCI continuous integration tools.

**Jasmin** is a test behavior driven development framework for testing javascript. It plays very well with karma. Similar to karma jasmin is also recommended as a framework of choice for AngularJS testing. Jasmin is dependency free.

### Practical fun

Repo already have karma packages and its dependencies \(karma-jasmine, jasmine-core, karma-chrome-launcher\) so simple npm command is sufficient to setup project.

```bash
npm install
```

I have configure package.json to run \`bower install\` command on post install of npm packages. while npm is doing its process you must need to install karma command line tool so open another terminal and run following command:

```
npm install -g karma-cli
```

At this point we have install karma and jasmin both, we are ready to create our karma configuration file so we can start writing tests. In terminal run following command:

```
karma init
```

It command will ask you series of questions just npm init do, In the end of command it will generate a config file for karma \_karma.conf . \_File should be looking like this:

```
module.exports = function(config) {
  config.set({
    basePath: '',
    frameworks: ['jasmine'],
    files: [
    ],
    exclude: [
    ],
    preprocessors: {
    },
    reporters: ['progress'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ['Chrome'],
    singleRun: false,
    concurrency: Infinity
  })
}
```

**Note: **do not forget to update files field in .conf file for angular and its dependencies.

## Writing tests

There are rules to write structured test projects:

1. Each module must contains there own tests for angular service, directive, factory, controller, component and filters.
2. Test must be inside test directory of each module.
3. it must have naming convention like _yourservice.\_spec.js or \_yourdirective_.spec.js etc.
4. And important of all **do not forget test directory to include in karma.conf file :\)**

Lets first write tests for login module in angular app. For simplicity of code I am taking three test cases for it.

1. Ensure invalid emails do not pass.
2. Ensure valid email pass the validation
3. Ensure path changes on user logged in.

> AngularJS also provides the [`ngMock`](https://docs.angularjs.org/api/ngMock) module, which provides mocking for your tests. This is used to inject and mock AngularJS services within unit tests. In addition, it is able to extend other modules so they are synchronous. Having tests synchronous keeps them much cleaner and easier to work with. One of the most useful parts of ngMock is[`$httpBackend`](https://docs.angularjs.org/api/ngMock/service/$httpBackend) , which lets us mock XHR requests in tests, and return sample data instead.

Please open client/app/login/test/controller.spec.js file to see all test cases. Files is well documented.





