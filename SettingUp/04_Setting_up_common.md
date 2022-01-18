### Setting up common

Next you need to set up `common`, a set of make scripts that enables you to more easily manage, build, check and publish packages.

For a cleaner `$HOMEDIR` it's suggested to have a folder where you are building your packages, this folder does not have to be inside your `$HOMEDIR`.

for setting up a folder inside your `$HOMEDIR` create a `Packaging` folder manually or via your terminal in your desired folder path.

You need to clone the common repository with git in the same directory you will have sub-folders for packages you are building, by running:
``` bash
git clone https://dev.getsol.us/source/common.git
``` 

Next you need to set up symlinks. Do this from the same directory you executed the `git` command:

``` bash
ln -sv common/Makefile.common .
ln -sv common/Makefile.toplevel Makefile
ln -sv common/Makefile.iso .
```

### Updating common

you have to update occasionally the `common` folder, because the Solus developer may update the scripting or add new features to help you with packaging. 

To update you `common` you have to `cd` into it via terminal and run the following command:

``` bash
git pull
``` 