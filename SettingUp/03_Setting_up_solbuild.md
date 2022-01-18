## Using solbuild

The `solbuild` tool must first b initialized with a base image. All builds thereafter will use this as a base, and construct a temporary overlay root to save on time and disk space in builds.

### Initializing solbuild

First, install the system.devel component by calling via your terminal

```bash
sudo eopkg install -c system.devel
```

Next, you need solbuild itself with

```bash
sudo eopkg install solbuild
```

If you are building against unstable repo, also install

```bash
sudo eopkg install solbuild-config-unstable
```

Next, you need to initialize solbuild via 

```bash
sudo solbuild init
```

This will take some time as it downloads and prepares the image. It is a good idea to update the root on a semi-regular basis, otherwise the updates will be applied on every build.

### Updating solbuild

t is a good idea to keep the base image updated. It will help reduce build times by not having to repeatedly download updates to packages in the base image, and will strictly need to pull down the packages your build needs.

To update solbuild, run:

```bash
sudo solbuild update
```

### Cleaning cache from solbuild

Sometimes you have solbuild errors on build time or your hard drive just gets full. 

To delete your solbuild cache, run:

```bash
sudo solbuild dc
```

Do you want to delete ccache, packages and sources, run:
```bash
sudo solbuild dc --all
```