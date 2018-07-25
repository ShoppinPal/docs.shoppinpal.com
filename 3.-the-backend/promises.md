# Promises

If you aren't familiar with promises as a concept then you have two choices: a\) follow instructions and use the code to get a desired effect, without a deep understandign of why it works, or b\) brush up: [https://www.promisejs.org/](https://www.promisejs.org/)

There are many prominent libraries that implement the concept of a `promise`. Our favorite in this tutorial will be [bluebird](https://github.com/petkaantonov/bluebird/blob/master/API.md).

To install this module, run the commands:

```text
$ cd ~/workspace/loopback-zero-to-hero
$ npm install --save --save-exact bluebird
```

in the terminal now.

The [really really long running discussion](https://github.com/strongloop/loopback/issues/418) around adding support for promises within loopback server side code and the [changelogs](https://github.com/strongloop/loopback-datasource-juggler/blame/master/CHANGES.md), let us draw the following semi-sure conclusions:

a\) If you are running on Node.js version `0.10.x`, then you need to add the following line to the top of your main `server/server.js` file to tell LoopBack which Promise implementation to use: `global.Promise = require('bluebird');`

b\) Version `2.19.0` of `loopback-datasource-juggler` was the first version to add Promises to DAO.

c\) Version `2.24.0` of `loopback-datasource-juggler` was the first version that added further by promisifying model relation methods.

d\) In \[package.json\]\(open\_file loopback-zero-to-hero/package.json panel=1 ref="loopback-datasource-juggler"\) we use Version `2.32.0` of `loopback-datasource-juggler`, its sufficient to say that the CRUD methods for models and relatedModels now use promises ... but something like `UserModel.login()` still does not!

e\) Let us promisify what the framework hasn't. Open \[user-model.js\]\(open\_file loopback-zero-to-hero/common/models/user-model.js"\) and update it:

```text
var Promise = require('bluebird');

module.exports = function(UserModel) {

  // https://github.com/strongloop/loopback/issues/418
  // once a model is attached to the data source
  UserModel.on('dataSourceAttached', function(obj){
    // wrap the whole model in Promise
    // but we need to avoid 'validate' method
    UserModel = Promise.promisifyAll(
      UserModel,
      {
        filter: function(name, func, target){
          return !( name == 'validate');
        }
      }
    );
  });

};
```

f\) Next, create 03-login-users.js: `touch ~/workspace/loopback-zero-to-hero/server/boot/03-login-users.js`

g\) Then add the following to [03-login-users.js](https://github.com/shoppinpal/docs-shoppinpal-com/tree/8cdd099563d11c1fe1df4d584b504337850c59eb/loopback/open_file%20loopback-zero-to-hero/server/boot/03-login-users.js):

```text
'use strict';
var Promise = require('bluebird');

// to enable these logs set `DEBUG=server:boot:03-login-users` or `DEBUG=server:boot:*`
var path = require('path');
var fileName = path.basename(__filename, '.js'); // gives the filename without the .js extension
var log = require('debug')('server:boot:'+fileName);

module.exports = function(app) {
    var UserModel = app.models.UserModel;
    var commentsIndex = 0;
    Promise.delay(3000).then(function(){
        UserModel.loginAsync(
            {username: 'admin', password: 'admin'}
        ).tap(function(accessToken) { // create a default/empty report for merchant1
            log('(' + (++commentsIndex) + ') ' + 'created', 'AccessToken', JSON.stringify(accessToken, null, 2));
            log('(' + (++commentsIndex) + ') ' + 'logged in w/ token ' + accessToken.id);
        });
    });
};
```

\|\|\|info

## info

Note the use of `UserModel.loginAsync()` and `.tap()`, both of which are made possible by the use of `bluebird` \|\|\|

h\) Now run and observe the logs:

```text
$ DEBUG=server:boot:*,boot:02-load-users node .

Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/

  server:boot:01-seed-data Its alive! +0ms
  boot:02-load-users Creating roles and users +2ms
  boot:02-load-users created role +499ms admin
  boot:02-load-users found user +1ms admin
  boot:02-load-users created role +2ms users
  boot:02-load-users found user +1ms user
  server:boot:03-login-users (1) created +3ms AccessToken {
  "id": "iumwgdnjmkavYYADlYF5miDA0d1pFWf13Dlzgvm7p9ptkRihSIi9PwkDJxtsc97H",
  "ttl": 1209600,
  "created": "2015-07-05T02:49:10.961Z",
  "userId": 2
}
  server:boot:03-login-users (2) logged in w/ token iumwgdnjmkavYYADlYF5miDA0d1pFWf13Dlzgvm7p9ptkRihSIi9PwkDJxtsc97H +0ms
```

i\) You can now use the access token spat out in the log lines: `logged in w/ token ...` where long strings like: `iumwgdnjmkavYYADlYF5miDA0d1pFWf13Dlzgvm7p9ptkRihSIi9PwkDJxtsc97H` represent an accessToken.

