Activator 1.3.2 based on OpenJDK 1.7 and Centos 6
=================================================

This is a minimal Docker image which provides a typesafe `activator 1.3.2`.
It is designed to launch play applications 2.3+ in Production mode with some security settings : beware some work still remains to be a proof secure platform !

This is based on the the Dordoka Activator image for Unbuntu 14.01.
See https://registry.hub.docker.com/u/dordoka/play-framework/

# Description
After building the image, you should run your container with some options. The entire process is described below.

##Includes:

 - Latest and updated Centos 6
 - Latest OpenJDK 1.7
 - Typesafe Activator 1.3.2
 - a play user isolating the activator running daemon and apps

##TODO:

 - Optimize settings : remove unneeded packages, upgrade to Oracle JVM (?!),...
 - Secure settings : work on the sudoers config and other config files for sure


## Users
A user named `play` is created with sudoers privileges. Its password has been locked that means loggin is only possible using SSH key. A session is automatically opened at container startup.

## Volumes
Mounts a volume on `/appli/play-app` to a local directory containing your Play application code.

## Ports
The internal `9000` default Play port is exposed to the `80` http default one.
This is done on command line at startup and can be easily changed.

# How to run the image
## Using docker v1.3+

Here is an example of a docker run command:

```
docker run --rm -it \
		-v "/path/to/your/play/app:/appli/play-app" \
		-p 80:9000 \
		jeanjerome/activator-1.3.2
```

Don't forget to adapt `/path/to/your/play/app` to your need.

# How to start your Play app
On the play user prompt, enter :

```
activator start

```

When the build is finished and your application started you should see :

```
[INFO] play - Application started (Prod)
[INFO] play - Listening for HTTP on /0:0:0:0:0:0:0:0:9000
```

## Image inheritance

This docker image inherits from the `jeanjerome/java-1.7.0-openjdk:1.0.0` image. It includes the `openjdk 1.7` installation on a `centos 6` in its latest version.