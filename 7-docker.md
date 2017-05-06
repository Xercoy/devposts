Man, Docker is a doozy. Having to Google everything Docker once in a while is exactly why this blog exists. By no means is this article a guide for newbies and should instead be utilized as a refresher.

# The Basics

### Summary

Read the official docs on everything Docker. It's a way better resource than anything I can summarize in the same number of words. In short, the `instance` or smallest, most basic instance of what runs in Docker is a `Container`. 

These `Containers` are based off of Docker `Images` which somewhat synonymous to an OS image. The `Images` are based off of `Dockerfiles`, a declarative and specific format of directives which setup the container (run this, copy this, here's where this is from, here's the name for the tag of the container, etc.). Use a `Dockerfile` to "extend" an existing `Image` as desired, build an `Image` from that, and run a container from that resulting `Image`... It's much better understood in practice.

### Installation
Head to the [Docker Store](http://store.docker.com) for information on how to download Docker. 

### Usage Example
Once that's up and running, the next most important piece is a Dockerfile. In this example, I'm going to create a container that will output hello world. Lines beginning with `#` are comments.
```
# The argument to the FROM directive denotes the organization/name of the entity in which the image should be pulled from. In this case it's the ubuntu image. More than one image can exist within an organization, denote the one you want in the format of <organization name>:<image version/type> 
FROM ubuntu

# This is a must have for all Dockerfiles, it's the cmd to run once the container is started.
CMD ["echo", "hello, world!"]
```

**Build the image: `$docker build -t test1 .`**

The command above will result in an image that is tagged with the name test1, hence the `-t` option.

**Run a container from the image: `$docker run test1`**

The command above will result in `hello world` being output, and the command will then exist. This is because the container shuts down if there isn't any process running in the foreground. 

**Of course**, there are so many options that exist within a Dockerfile + `docker` commands which can be run to start a container. 

Say we have a Go web server that we'd like to run. Look for an existing image online on [`Docker Hub`](https://hub.docker.com/_/golang/) which should have Go installed, otherwise it's totally acceptable to include directives to install it. In this case, I used an `Alpine` based image which runs Go 1.8. See [here](https://hub.docker.com/_/golang/) for more specific information.
```
# What image is this Dockerfile based on?
FROM golang:1.8.1-alpine

# What is the working directory of the container?
WORKDIR /app

# Copy the files within the current directory that the Dockerfile is in to the specified directory.
ADD . /app 

# Make port 8043 available to the outside container
EXPOSE 8043

# Run the web server
CMD ["go", "run", "main.go"]
```

**Build the image: `docker build -t mygoapp .`**

**Run the container: `docker run -p 8080:8043 -d mygoapp`**

The `-p` option maps a local port to a specified port in the container. 

The `-d` option runs the container in detached mode, in other words, in the background. 

Remember how a container exists if there isn't any  process running in the foreground? Add `-t` and you're all set.

### Useful Links/Resources
[Amazing Post on Building Minimal Docker Images](https://blog.codeship.com/building-minimal-docker-containers-for-go-applications/)

[Docker Overview from Digital Ocean](https://www.digitalocean.com/community/tutorials/docker-explained-using-dockerfiles-to-automate-building-of-images)

[Docker Stopping After Docker -d](http://stackoverflow.com/questions/30209776/docker-container-will-automatically-stop-after-docker-run-d)

[After importing an image, run gives "no command specified](https://github.com/moby/moby/issues/1826)

[Golang Docker Hub Page](https://hub.docker.com/_/golang/)

[Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet#exposing-ports)

# Docker Hub

## Pushing an image to docker hub 

Check out the official doc page [here](https://docs.docker.com/docker-cloud/builds/push-images/)

1) Login - `$ docker login`

2) Tag the image - `$ docker tag my)image <docker user ID>/<image name>

3) Push it - `$ docker push <docker user ID>/<image name>

===

### Docker Cheat Sheet
---

### Other Notes
---


