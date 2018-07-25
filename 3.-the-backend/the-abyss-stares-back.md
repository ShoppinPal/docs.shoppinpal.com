# The abyss stares back

1. Open a new terminal window \(`Tools > Terminal`\) so that we don't have to stop the loopback server.
2. `$ cd ~/workspace/loopback-zero-to-hero/`
3. Take a peek at the database: `cat db.json`

   ```text
    $ cat db.json
    {
      "ids": {
        "User": 2,
        "AccessToken": 1,
        "ACL": 1,
        "RoleMapping": 1,
        "Role": 1
      },
      "models": {
        "User": {
          "1": "{\"username\":\"test\",\"password\":\"$2a$10$Iy6R6/GRUq7g.xIZnx8qWuzkYuFR75XjIgSpdb6k3fmuC3w07u1Bq\",\"email\":\"test@test.com\",\"id\":1}"
        },
        "AccessToken": {},
        "ACL": {},
        "RoleMapping": {},
        "Role": {}
      }
    }
   ```

