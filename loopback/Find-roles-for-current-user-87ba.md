a) Update the `relations` block of `common/models/user-model.json` file like so:
```
  "relations": {
      "roles": {
          "type": "hasMany",
          "model": "Role",
          "through": "RoleMapping",
          "foreignKey": "principalId"
      }
  },
```

b) But before we can test this, we need as `accessToken` to use in the UI explorer to make the call. How can we do that?
We can resuse the one we retieved in the last section from the logs.

c) Start the server with:
`cd ~/workspace/loopback-zero-to-hero/ && DEBUG=server:boot:*,boot:02-load-users node .`

```
$ cd ~/workspace/loopback-zero-to-hero/ && DEBUG=server:boot:*,boot:02-load-users node .
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
  server:boot:01-seed-data Its alive! +0ms
  boot:02-load-users Creating roles and users +1ms
  boot:02-load-users found role +209ms admin
  boot:02-load-users found role +0ms users
  boot:02-load-users found user +1ms admin
  boot:02-load-users found user +3ms user
  server:boot:03-login-users (1) created +3s AccessToken {
  "id": "ACKQJqLNktnr1Rovsb3hluoGtqMiakSBrxntcdFKy6nEl29dsUYFksM4NUNQ9DHo",
  "ttl": 1209600,
  "created": "2015-07-06T21:37:56.821Z",
  "userId": 1
}
```

d) Copy a token string from the logs

e) Launch the browser at: `<public_url>:3000/explorer`

f) Paste the token into the textbox on the top right of the explorer UI and click the `Set Access Token` button

g) Access the roles via an api call at:
`<public_url>:3000/explorer/#!/UserModels/findById`

g.1) fill in the `filter` field with: `{"include":"roles"}`

g.2) as for the `id` field, you can pick out its value from the logs around the same place you found the access token, look for `userId` in the logs:
```
server:boot:03-login-users (1) created +3s AccessToken {
  "id": "ACKQJqLNktnr1Rovsb3hluoGtqMiakSBrxntcdFKy6nEl29dsUYFksM4NUNQ9DHo",
  "ttl": 1209600,
  "created": "2015-07-06T21:37:56.821Z",
  "userId": 1
}
```
g.3) Click the `Try it out!` button and you should see a response like:
```
{
  "username": "admin",
  "email": "admin@admin.com",
  "id": 1,
  "firstName": "Admin",
  "lastName": "User",
  "roles": [
    {
      "id": 1,
      "name": "admin",
      "created": "2015-07-05T03:06:07.989Z",
      "modified": "2015-07-05T03:06:07.989Z"
    }
  ]
}
```
which has the roles information included in it.