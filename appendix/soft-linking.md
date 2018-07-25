# Soft Linking

* `ln -s <source> <destination>`
  1. if a folder will go inside a preexisting destination folder then use
     * `ln -s /path/to/source/ /path/to/destination/`
  2. if a folder will become a destination folder then use
     * `ln -s /path/to/source/ /path/to/destination`
  3. when soft linking the source path must be reachable as-is from the destination ... for example:
     1. if server folder resides at `~/dev/project/server` and we want to put a soft linked version of it under the `~/dev/project/linkUnderMe/` folder as `~/dev/project/linkUnderMe/server`
        1. ~/dev/project/server
           * exists
        2. ~/dev/project/linkUnderMe/
           * exists
        3. ~/dev/project/linkUnderMe/server
           * this soft link is what we want to accomplish
     2. then
        1. go to `cd ~/dev/project/` and try
        2. `ln -s ./server ./linkUnderMe/server`
           1. but it will NOT work!
           2. because `./server` is not reachable from inside of `./linkUnderMe/` as-is
        3. `ln -s ./../server ./linkUnderMe/server`
           * will work
        4. `ln -s ~/dev/project/server ./linkUnderMe/server`
           * will work

