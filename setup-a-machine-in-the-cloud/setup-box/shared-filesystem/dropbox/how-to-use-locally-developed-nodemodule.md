#Use locally developed node module in another project

##Prerequisite
- Docker


##Here goes:
If you're working on developing a node module(Let's call it `project1`), and also want to try it in some other project locally(Let's call it `project2`), then you might be worried about going through the whole process of publishing it to npm.

Or write efficient tests for the module, and be confident enough that it'll work in another project no matter what.

Or moreover, you might just copy the module into your node_modules folder, and repeat it until your brain says it sucks to copy the whole thing all the time.

Or be a smart ass, and follow these simple steps (This only works with projects using docker, so shift your projects to docker today):


##Steps to be smart:
- Go to the docker-compose.yml file of your project2.
- Find the container where you want to use the project1.
- It should be something like this:
```
service_name:
    build:
      xxx: xxx
    working_dir: xxx
    command: xxx
    blah:  
    blah:
```

- Set up an attribute `volume` here. `volume` allows you to mount host paths or named volumes, specified as sub-options to a service.
```
service_name:
    blah:
    blah:
    volume: 
       /path/to/project1/:/path/to/node_modules/project1
```

- This mounts project1 inside the container `service_name`. You can go verify it by logging into the container machine once it is up and running. Here's the handy command `docker-compose run service_name /bin/bash`.
- Once you enter the container machine, go see your code sync realtime at `/path/to/node_modules/project1`.

You're welcome ;)
