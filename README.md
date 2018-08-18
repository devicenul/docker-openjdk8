# Docker [mercnet/openjdk8-jdk | mercnet/openjdk8-jre]

Java OpenJDK image with a few essential additions to the base CentOS Image.

This repository is setup to build the image using the images with the fabric8.io 
docker-maven-plugin.  The building of the image is associated with the 
package phase and the push of the image is associated with the install 
phase.  Hence the dockerfile is located in 

    <project root>/src/main/docker/Dockerfile

The **DOCKER_HOST** is configured to be tcp://localhost:2375  This can be overriden
by set the **DOCKER_HOST** environment variable before executing the maven commands.
 
## How to run

#### Prerequirements - Docker

Install `docker` according the instructions at 

#### Get pre compiled image

    docker pull mercnet/openjdk8-jdk:latest
#### Run

    docker run -rm -it mercnet/openjdk8-jdk /bin/bash

#### or build your own from repository
    
    mvn -P docker package
    docker run --rm -it mercnet/openjdk8-jdk /bin/bash
    
#### or to manually publish the image to the docker registry

    mvn -P docker validate initialize docker:push

## What's in this container?