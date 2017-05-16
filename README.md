# Maru OS Container Blueprints

[![Build Status](https://travis-ci.org/maruos/blueprints.svg?branch=master)](https://travis-ci.org/maruos/blueprints)

Container image builder for Maru OS.

### Blueprints

Image building logic is separated into standalone plugins called blueprints.

To create your own blueprint, all you need to do is:

1. Add a directory under blueprint/. Use this directory to store anything you
   need during the build process.

2. Add a script called plugin.sh to the top-level of your new blueprint
   directory. This will be the entrypoint to your blueprint.

3. Define the function `blueprint_build` in plugin.sh that will run your build
   logic.

4. Define the function `blueprint_cleanup` in plugin.sh that will clean up any
   intermediate build artifacts.

## Prerequiste

```
apt install qemu-user-binfmt qemu-user-static debootstrap curl cgmanager
update-binfmts --importdir /var/lib/binfmts/ --import
update-binfmts --install qemu-arm
update-binfmts --enable
```

### Examples

Build a Kali armhf container called 'kali' (option defaults):

    # ./build.sh -b kali -n kali-rolling -- -a armhf

Build a Kali arm64 container called 'kali-rolling64':

    # ./build.sh -b kali -n kali-rolling -- -a arm64

Docker build:

	# docker build -t lxcbuilder .
	# docker run -ti --privileged=true lxcbuilder

*Tip: You will need root privileges to mount binfmt_misc for bootstrapping
foreign architecture containers.*

### Contributing

See the [main Maru OS repository](https://github.com/maruos/maruos) for more
info.

### Licensing

This repository is licensed under the Apache License, Version 2.0. See
[LICENSE](LICENSE) for the details.
