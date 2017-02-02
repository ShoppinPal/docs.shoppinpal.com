# Unit Testing of Angular \(karma + jasmin\)

TDD is essential part of any software development. I tell you a my experience why it is so important, I created a filter module for product just like amazon or flipkart have. I tested it well on my machine and it was working great, now it is the day of live demo to client. In live demo filter suddenly stopped working, it was doing nothing in staging env it was kind of embarrassing. The day after that I decided to write unit test for each every function that I wrote. As a developer I feel confident in my code to run, a developer must learn to love the feeling of having a water-tight app.

Apart from my stories lets start real example. You can follow [AngularUnitTestDemo](https://github.com/Mohammed-Aadil/AngularUnitTestDemo) on github or clone a local copy to begin with.

## Moto behind this blog

This blog contains fundamentals of angular unit testing that we are using in [Shoppinpal](/www.shoppinpal.com). It beginner guide for developer and tester on unit testing. At the end blog you would have sufficient knowledge for created simple unit testing in angularJS.

## How to write the test

Everyone has same question the one who writing test for first time. You must break down your logic of your application to small chunks or unit and verify each chunks work perfectly and as desired. **In javascript the smallest individual chunk you can test are usually functions. The core feature in application must verified with accompanying of unit tests. **Unit testing must be done on base of input and output of individual function so when they are joined together it has better chance to have worked as whole, it is better not to interfere with operation of function.

Best practice says you should write your unit test before actual development starts. You must have question in mind how you can do it? Answer for it is simple just create an empty unit test for function and keep it updating as function gets updated and freeze it when final move is made on that function development. So if any new comer comes and try to change in code he/she would know logic break in tests.

Unit tests must be break down into 3 parts:

1. Story
2. Feature
3. Units

So in our case Story is \`_User comes to our page and login to it, successful he redirected to Profile page_\`. In this we says feature is user login and we further divide feature into units as following:

1. Ensure invalid emails do not pass.
2. Ensure valid email pass the validation.
3. Ensure path changes on user logged in.

```
describe("user login form", function() {
    it("Ensure invalid emails do not pass", function() {});
    it("Ensure valid email pass the validation", function() {});
    it("Ensure path changes on user logged in", function() {});
});
```

## Configuring karma + jasmin for our angular app

### Introduction to tools

**Karma **is test runner and it is a direct product from angularJS team. It provide flexibility to test your app in various browser and get integrated with Jenkins, TravisCI and CircleCI continuos integration tool.

**Jasmin **is test behavior driven development framework for testing javascript. It plays very well used with karma. Similar to karma jasmin is also recommended testing framework choice for angularJS testing. Jasmin is dependencies free.

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





