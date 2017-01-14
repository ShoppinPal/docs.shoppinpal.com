You should see two new files:
```
$ cd ~/workspace/loopback-zero-to-hero  
$ tree common -L 3
common
└── models
    ├── user-model.js
    └── user-model.json

1 directory, 2 files
```

Take note of the following:
a) `user-model.json` has the following lines:
```
  "name": "UserModel",
  "base": "User",
```

b) the files are named `user-model.js` and `user-model.json` but the internal name used by code is `UserModel`, this is part of loopback's naming convention.

c) `user-model.json` serves as a configurable entry point whereas `user-model.js` lets you add code when something more specialized may be required, something that can't be simply configured.

d) Moving forward we will always use `UserModel` so we can and should hide the `User` model from the prying eyes of our REST~ful api.

e) The `server/model-config.json` file is the gatekeeper for what's exposed over REST and what's not.
```
cat ~/workspace/loopback-zero-to-hero/server/model-config.json
{
  ...
  "User": {
    "dataSource": "db"
  },
  ...
  "UserModel": {
    "dataSource": "db",
    "public": true
  }
}
```

f) Go ahead and set `"public": false` for `User` in `model-config.json` file:
```
{
  ...
  "User": {
    "dataSource": "db",
    "public": false
  },
  ...
}
```

g) Fire up the server:
```
$ cd ~/workspace/loopback-zero-to-hero
$ node .
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
```

h) `Project > Box Info`

i) Open a browser window: `http://<box-name>.codio.io:3000/explorer/`

j) The `UserModel` api will be ready to explore and `User` will be no more!

k) Use `/POST UserModels` from the explorer UI to create a user:
```
    {
      "username": "test",
      "password": "test",
      "email": "test@test.com"
    }
    ```
    Use that as the json body and then click the `Try it out!` button.
```

l) There is a distinct possiblility that your server will crash at this point with `TypeError: Object.keys called on non-object`

Here's the full sample stack trace:
```
events.js:72
        throw er; // Unhandled 'error' event
              ^
TypeError: Object.keys called on non-object
    at Function.keys (native)
    at Memory.all (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/connectors/memory.js:315:22)
    at /home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/dao.js:1453:19
    at doNotify (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:93:49)
    at doNotify (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:93:49)
    at doNotify (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:93:49)
    at doNotify (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:93:49)
    at doNotify (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:93:49)
    at Function.ObserverMixin._notifyBaseObservers (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:116:5)
    at Function.ObserverMixin.notifyObserversOf (/home/codio/workspace/loopback-zero-to-hero/node_modules/loopback-datasource-juggler/lib/observer.js:91:8)
```
|||guidance
# Guidance

If this happens, simply delete the previous `db.json` file:
`rm ~/workspace/loopback-zero-to-hero/db.json `
And start the server again, then Follow steps (g) through (k) again.
|||

m) Take a peek at the database, it should have a new UserModel instance: `cat db.json`
```
$ cat db.json
{
  "ids": {
    "User": 1,
    "AccessToken": 1,
    "ACL": 1,
    "RoleMapping": 1,
    "Role": 1,
    "UserModel": 2
  },
  "models": {
    "User": {},
    "AccessToken": {},
    "ACL": {},
    "RoleMapping": {},
    "Role": {},
    "UserModel": {
      "1": "{\"username\":\"test\",\"password\":\"$2a$10$DD6l9hEK0YraAvQ9wxXoyujLyted4YUUOUX9opiTUe8RwPOGe8mY2\",\"email\":\"test@test.com\",\"id\":1}"
    }
  }
}
```
