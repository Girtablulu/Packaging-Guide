# Building a Package

This guide will walk you through setting up the files(s), tooling and building your package.

## Setting up Packager file

in order to utilise the build system, you must first set up a configuration file that has your packager details, the file has to be only set up if you'd like to help Solus in maintaining packages.

This file lives in the `solus` folder of your home config directory. You will need to create the `solus` folder as well as the inner `packager` file. inside the packager file, you need two keys `Name` and `Email`. This is used when generating the machine file so that the packager details are stored within the resulting binary package.

you can either create the folder manually with your filemanager under, you may have to show hidden folders in your filemanager settings

``` bash
$HOME/.config/solus
```

or via terminal

``` bash
mdkir -p .config/solus
```

after you created the folder you have to create the `packager` file within


``` ini
[Packager]
Name=Your Name Here
Email=your.email@address
```
