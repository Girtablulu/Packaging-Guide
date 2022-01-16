# New packaging guide for Solus

## Goals

- One file to rule them all
- Simple to follow instruction (so terminal beginner can follow them)
- You should be able to package something by just scrolling down
- Separate beginner and advance usage
- Generall Information which arent crutial to packaging can be in a separate file
- Having just once example not multible to less confuse stuff
- Agrement to similar word usage (exampl. diff/patch)

# Proposed structure

## Generell information about the infrastuctur we are using (link to another file?)
- solbuild
- common
- phabricator
   - Repo
   - Diff
   - Maintainer
- IRC: Solus-Dev

## Setting up everything

### Beginner set up for packaging

- Setting up Packager file
- Setting up solbuild
   - update solbuild
- Setting up common
   - update common file

### For submitting the package

- setting up Archanist

### Advanced set up for packaging

- Setting up a local repo
- Setting up a custom repo
  - manuall indexing
  - creating custom profiles

## How to Build a package using solbuild

- How is a Package.yml is set up (link to another file?)

### Beginner packaging

- Generating a Package.yml
- Which information have to be provided (lisense, infos etc.)
- How to search for builddeps/rundeps
- different Macros (link to another file?)
- How to build your package
- Bumping a Package
- How to check your .eopkg file for issues
- Maintainer file creating

### Advanced packaging

- installing extra files from source
   - creating own extra files
   - tmp files
- Patterns
- Replace/rename
- How to use a patch
   - command %patch
   - command %apply_patches
   - Security Patch
- How to add an upstream patch
   - command wget
- How to create your own patch from code

## How to update a package

- Update alias
- respect the Maintainer file

## How to Submit a package

### Submitting a package

- What needs to be done before submitting (Checks)
   - version/release
   - abi changes
   - path changes
   - Check if on the correct commit
- Creating the diff
- Submitting for Review
- Submitting stacks
- Updating Task Information


### Updating a a submitted diff

- what to do reg the changes
- how to recreate the diff
- squashing commits


