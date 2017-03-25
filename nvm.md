# nvm

The Node Version Manager or `nvm` in short is a great tool.

We could debate the pros and cons of `switching between multiple versions of NodeJS & NPM` versus `dockerized containers for each specific version of NodeJS & NPM` but we won't tackle that here.

Instead we will focus on a common use case for those who are used to `switching between multiple versions of NodeJS & NPM.`

For those developers who are working across multiple nodejs projects, each with a different version ... you may end up running one of the projects using a version that wasn't meant for it. It can be tricky to remember and switch the version via `nvm` per terminal window/tab. Luckily this can be automated by leveraging the metadata from `.nvmrc` file in your projects.

My solution isn't a solution generic enough but I mixed together the previous suggestions from this [thread](https://github.com/creationix/nvm/issues/110) with stackoverflow to add the following for `mac/osx` in my `~/.bash_profile` and it worked well:

```
# change title name of tab in terminal
function title {
    echo -ne "\033]0;"$*"\007"
}

cd() {
  builtin cd "$@" || return
  #echo $PREV_PWD
  if [ "$PWD" != "$PREV_PWD" ]; then
    PREV_PWD="$PWD";
    title $(echo ${PWD##*/}) $(node -v);
    if [ -e ".nvmrc" ]; then
      nvm use;
      # set tab terminal name to be cwd and node version
      title $(echo ${PWD##*/}) $(node -v);
    else
      nvm use default;
    fi
  fi
}
```

Now I can do:

```
# I always switch to the default version `v0.10.44`
# when I go to a folder that does not have `.nvmrc`
$ cd ~/dev/
Now using node v0.10.44

# If `.nvmrc` exists then the version is switched
# to the one specified in that file.
$ cd ~/dev/ts-sandbox-2/
Found '~/dev/ts-sandbox-2/.nvmrc' with version <4>
Now using node v4.4.7

# and again
$ cd ~/dev/
Now using node v0.10.44
```
