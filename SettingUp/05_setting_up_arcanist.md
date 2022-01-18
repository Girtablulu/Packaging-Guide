#### Setting up Arcanist

for sending your updateed package.yml for review for Solus you need to set up Arcanist, additionally you need an Account on Phabricator

First visit [Solus Phabricator](https://dev.getsol.us/) and create an account, which will be used to communicate with you while the patch review.

Next you have to install `Arcanist`, run:

``` bash
sudo eopkg it arcanist
```

Next you have to set the config to Solus

``` bash
arc set-config default https://dev.getsol.us
```

Next install the certificate, on the third step you will be given a unique link to log into the Developer Portal, to create a `Conduit API Token`. This token will be used to allow the CLI `arc` utility to communicate with Phabricator.

``` bash
arc install-certificate
```

