# How it all ties together: cli, npm, package.json, pretest, test, mocha

My Gist:
https://gist.github.com/pulkitsinghal/d53ad3538e153e6003a99139715beed3

Reading Material:
- http://www.marcusoft.net/2015/08/pre-and-post-hooks-for-npm-scripting.html
- http://www.marcusoft.net/2015/08/npm-scripting-configs-and-arguments.html#passing-through-command-line-argument

Even docker mixes npm scripts with docker and mocha tests very well:
https://engineering.gosquared.com/testing-with-docker

Some people prefer to use `grunt` commands to make it easy, like: `grunt test:e2e` can be setup and configured to take care of running all tests without knowing much about underlying stuff. But it would be nicer if same could be [accomplished via the scripts](http://www.kramnameloc.com/getting-started-with-protractor) in `package.json` instead.