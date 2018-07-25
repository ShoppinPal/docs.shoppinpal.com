# Build a better mousetrap

* `$ cd ~/workspace/loopback-zero-to-hero/`
* If we inspect `server/datasources.json` out-of-the-box \(OOTB\), we should see that a memory database is in use as a mock placeholder of sorts. This is done so we may develop our application logic without worrying about the backend too early.

  ```text
    cat ~/workspace/loopback-zero-to-hero/server/datasources.json
    {
      "db": {
        "name": "db",
        "connector": "memory"
      }
    }
  ```

* Let's build a better mousetrap! Errrrr... database, Let's build a better database.

\|\|\|topic

## Database Connectors

Read official docs on [Database Connectors](http://docs.strongloop.com/display/public/LB/Database+connectors) \|\|\|

1. Using a file to back the memory DB has significant advantages.
2. We can look at what's going on behind the scenes by simply peeking into a json file
3. We don't lose all our data on every restart.
4. So let's edit `server/datasources.json` by adding a line `"file": "db.json"` to it:

   ```text
    {
      "db": {
      "name": "db",
      "connector": "memory",
      "file": "db.json"
      }
    }
   ```

5. Fire up the server: `node .`
6. `Project > Box Info`
7. Open a browser window: `http://<box-name>.codio.io:3000/explorer/`
8. The `Users` api will be ready to explore OOTB.
9. Use `/POST Users` from the explorer UI to create a user:

   ```text
    {
      "username": "test",
      "password": "test",
      "email": "test@test.com"
    }
   ```

    Use that as the json body and then click the `Try it out!` button.

