# Unit Testing

## Configuring karma + jasmin for our angular app

### Introduction to tools

**Karma** is a test runner and it is a direct product from angularJS team. It provides flexibility to test your app in various browsers and is integrated with Jenkins, TravisCI and CircleCI continuous integration tools.

**Jasmin** is a test behavior driven development framework for testing javascript. It plays very well with karma. Similar to karma jasmin is also recommended as a framework of choice for AngularJS testing. Jasmin is dependency free.

### Practical fun

The repo for [AngularUnitTestDemo](https://github.com/Mohammed-Aadil/AngularUnitTestDemo) already has karma packages and its dependencies \(karma-jasmine, jasmine-core, karma-chrome-launcher\) so a simple npm command is sufficient to setup the project:

```bash
git clone https://github.com/Mohammed-Aadil/AngularUnitTestDemo
cd AngularUnitTestDemo
npm install
```

I have configured `package.json` to run `bower install` command on post install of npm packages. While npm is running, you can install karma command line tool in parallel, so open another terminal and run the following command:

```
npm install -g karma-cli
```

At this point we have installed `karma` and `jasmin` both. We are ready to create our karma configuration file so we can start writing tests. In a terminal, run the following command:

```
karma init
```

This command will ask you series of questions, just hit enter to accept defaults. At the end, it will generate a config file for karma: `karma.conf`. This file should look like:

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

**Note:** do not forget to update the `files` field in `karma.conf` file for angular and its dependencies.
