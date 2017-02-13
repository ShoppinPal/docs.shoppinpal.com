# The Backend

## Setup a loopback project

To start with a clean environment, run:
```
$ mkdir -p ~/workspace
$ cd ~/workspace
$ rm -rf loopback-zero-to-hero
```

Make sure you have 

Next, setup a loopback project:
```
$ slc loopback
? What's the name of your application? loopback-zero-to-hero
? Enter name of the directory to contain the project: loopback-zero-to-hero
```
It will just a short while to finish.

### What just happened?

- A minimal set of files was placed in the `loopback-zero-to-hero` directory to facilitate your project development. And `npm install` was auto run as part of project setup.

- Let's take the time to understand our directory structure:
    ```
    $ cd ~/workspace/loopback-zero-to-hero
    $ tree -L 1                               
    .
    ├── client
    ├── node_modules
    ├── package.json
    ├── README.md
    └── server
    ```

- The `client` folder is meant to house the source code for your project's frontend/UI. If you look at it right now, it has nothing but a README file:
    ```
    $ cd ~/workspace/loopback-zero-to-hero
    $ tree -L 1 client
    client
    └── README.md
    ```
    for all intents and purposes, it can simply be considered empty.

- The `node_modules` folder contains dependencies which were installed based on what's listed in the `package.json` file. If you are unfamiliar with this concept, you will need to brush up on the basics of NodeJS and the purpose of `package.json` file.

- The `server` folder contains the bulk of your server-side logic which is where LoopBack shines! Take a peek:
    ```
    $ cd ~/workspace/loopback-zero-to-hero
    $ tree -L 2 server
    server
    ├── boot
    │   ├── authentication.js
    │   ├── explorer.js
    │   ├── rest-api.js
    │   └── root.js
    ├── config.json
    ├── datasources.json
    ├── middleware.json
    ├── model-config.json
    └── server.js
    ```
    - `boot` folder contains `js` files which will be run (alphabetically by default) when loopback starts
    - some configuration files that will be easier to understand if we explain them in sections that follow
    - `server.js` file is the entry-point for launching loopback. Just like any NodeJS application, you can run it with `node path/to/file.js`:
      ```
      $ node server/server.js
      Browse your REST API at http://0.0.0.0:3000/explorer
      Web server listening at: http://0.0.0.0:3000/
      ```
      press `ctrl+c` to exit.