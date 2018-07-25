# Boot Scripts

What if you have a file with all the users that should be added to your database before the server starts but only if they aren't present already? How would you leverage the LoopBack framewrok to accomplish this?

The answer is [boot scripts](http://docs.strongloop.com/display/LB/Defining+boot+scripts).

Boot scripts allow you to step into the loopback bootup process and do exactly that. By default they sit inside the `server/boot` directory.

Lets peek at what's already in there:

```text
$ tree ~/workspace/loopback-zero-to-hero/server/boot/

server/boot/
├── authentication.js
├── explorer.js
├── rest-api.js
└── root.js
```

Remember how you ran `slc loopback` in the very beginning? Those files represent what the `application generator` laid down for you by defualt to setup the project.

When adding more files to the `server/boot` directory, its important to understand the order in which they will be loaded or executed.

> The easiest way to specify the order of loading boot scripts is by scripts' file names, since LoopBack always executes boot scripts in alphabetical order. For example, you could name boot scripts `01-your-first-script.js`, `02-your-second-script.js`, and so forth. This ensures LoopBack loads scripts in the order you want, for example before default boot scripts in `/server/boot`.

So lets create a file named `01-seed-data.js`:

```text
$ touch ~/workspace/loopback-zero-to-hero/server/boot/01-seed-data.js
```

Open the file and add:

```text
var path = require('path');
var fileName = path.basename(__filename, '.js'); // gives the filename without the .js extension
var log = require('debug')('server:boot:'+fileName);

module.exports = function(app) {
    log('Its alive!');
};
```

Then run:

```text
$ npm install --save --save-exact debug
debug@2.2.0 node_modules/debug
└── ms@0.7.1

$ DEBUG=server:boot:* node .
  server:boot:01-seed-data Its alive! +0ms
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
```

Points to note: a\) The first three lines of code in `01-seed-data.js` do nothing more than create a specialized logging module known as `debug`. It can be turned on when its developer defined "namespace" \(`server:boot:*` in this case\) is specified via an environment variable named `DEBUG`.

b\) This add an extra line of log compared to what we are used to seeing: `server:boot:01-seed-data Its alive! +0ms` and confirms that our boot script is running.

c\) Even more important is to ask: Why didn't we just use `console.log()`? Because this syntax is used all over loopback to turn loggin on & off and its best to get used to this early on to make your own life easier.

d\) Go ahead stop the server \(`ctrl+c`\) and then start it with: `DEBUG=loopback:* node .`

What happens? Do you see a boat load worth of logs scrollign by? Well, we just turned on all the logs that fall under the `loopback:*` namespace! This can be quite useful when debugging, if you know which namespace you are after specifically.

e\) Let's narrow the scope a bit. Go ahead stop the server \(`ctrl+c`\) and then start it with: `DEBUG=loopback:boot:executor,server:boot:* node .`

We decided that we want information on two specific napespaces: `loopback:boot:executor` and everything that falls under `server:boot:*` and that's what you should see in your logs now.

There will be a lot of logs for `loopback:boot:executor` but somewhere in there you should be able to find a single line that states: `server:boot:01-seed-data Its alive! +0ms`

And if you look on line above and one below it, its position in the logs should make a lot of sense because the file was jsut loaded by the executor:

```text
loopback:boot:executor Starting sync function /home/codio/workspace/loopback-zero-to-hero/server/boot/01-seed-data.js +0ms
server:boot:01-seed-data Its alive! +0ms
loopback:boot:executor Sync function finished /home/codio/workspace/loopback-zero-to-hero/server/boot/01-seed-data.js +1ms
```

Anyhow, lets start main event.

Go ahead stop the server \(`ctrl+c`\).

We will now downlaod a boot script to create users and roles for us:

```text
cd ~/workspace/loopback-zero-to-hero/server/boot && curl -O https://raw.githubusercontent.com/beeman/loopback-angular-admin/master/server/boot/02-load-users.js
```

Once the file has been downloaded, revert back to the project directory: `cd ~/workspace/loopback-zero-to-hero`

Have a peek at [02-load-users.js](https://github.com/shoppinpal/docs-shoppinpal-com/tree/8cdd099563d11c1fe1df4d584b504337850c59eb/loopback/open_file%20loopback-zero-to-hero/server/boot/02-load-users.js;), its quite a useful script from the github user [@beeman](https://github.com/beeman)

Find this line in [02-load-users.js](https://github.com/shoppinpal/docs-shoppinpal-com/tree/8cdd099563d11c1fe1df4d584b504337850c59eb/loopback/open_file%20loopback-zero-to-hero/server/boot/02-load-users.js;): `var User = app.models.User;` And change it to use our extended model instead: `var User = app.models.UserModel;`

Start the server with: `DEBUG=server:boot:*,boot:02-load-users node .` and have a look at the logs.

Hopefully, it just makes sense:

```text
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
  server:boot:01-seed-data Its alive! +0ms
  boot:02-load-users Creating roles and users +2ms
  boot:02-load-users created role +190ms admin
  boot:02-load-users created role +274ms users
  boot:02-load-users created user +262ms admin
  boot:02-load-users created user +2ms user
```

Peek at the [db.json](https://github.com/shoppinpal/docs-shoppinpal-com/tree/8cdd099563d11c1fe1df4d584b504337850c59eb/loopback/open_file%20loopback-zero-to-hero/db.json;) file as well. You should be able to spot the newly populated data.

