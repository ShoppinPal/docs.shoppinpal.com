The built-in `User` model is quite all right but many developers quickly find a need to extend it. The most common cause is the need to fetch all the entities related to a given user. For example:
a) find all the roles for the current user, or
b) find all stores that `belong to` the current user, or
c) find all suppliers that `belong to` the current user, or
d) find all reports that `belong to` the current user, etc.

There isn't a concrete naming convention for extended models but there are some practical considerations around what not to do.


You have the option of naming a `user` (lowercase) model which builds upon the built-in `User` model as its `base`. But personally that makes me far too uneasy as I feel that the possibility of mistakes around which model actually gets used, both in the loopback core code and developer code, skyrockets.

Instead let's name it `UserModel` instead, no room for confusion!

Create a new model: `common/models/user-model.json`
```
$ slc loopback:model

Just found a `.yo-rc.json` in a parent directory.
Setting the project root at: /home/codio/workspace/loopback-zero-to-hero

? Enter the model name: UserModel
? Select the data-source to attach UserModel to: db (memory)
? Select model's base class: User
```

|||warning
# Remember

Don't forget to set the model's base class as `user`
|||

Carry on:
```
? Custom plural form (used to build REST URL):
Let's add some UserModel properties now.

Enter an empty property name when done.
? Property name:
```
Leave the last prompt (`? Property name:`) empty and hit enter to finish model creation.

|||info
# Info

Hit the refresh symbol at the bottom right of the nav tree panel to see the new `common/models` directory and its contents listed.
|||
