---
sort: 1
---

# What is Docker

 * Without answering the question 'What is docker?', lets see what does docker provide us.
 * Docker provides us with the ability to package applications.
 * The packaged application (binary) is called as a docker image.
 * When the packaged application is run, the running instance of the packaged application is called as docker container.
 * Docker provides us with an infrastructure called docker registry to share/distribute packaged applicaitons (images).
 * Docker registry could be considered something similar to Android Play store or iOS app Store.
 * Docker hosts a docker registry called as [docker hub](https://hub.docker.com/)
 * Apart from docker, there are many other hostings of docker registry. Some private and some public.
 * Now coming back to Docker, Docker is this infrastructure that makes it possible to package applications, run the packaged application and then share/distribute it.

# Why Docker

Now that we have seen what is docker. Lets see why docker

## Portability of Docker
When an application is dockerized, it would be easy to run the application in nearly any machine where docker is installed. This drastically increases the portability. 

## Uninstalling/Removing of dockerized is easy and safe
Its quite easy to remove/uninstall dockerized applications. The removal is just by one command. When a dockerized application is removed, it does not leave any trace of it. This makes it highly secure.

## Running dockerized application is relatively safe
When running dockerized application, we have a very high degree of control on the ports that it is allowed to listen to and the areas of the file system it is allowed access. This makes it highly secure.

## Sharing/Publishing of application is made simpler: 
 Docker registry provides an easy way to share/publish application. This lets us download an application with just one command.

## Simplifies local development setup:
 When an organization develop system, it would contain different components, and different components are often developed in different languages. So one developer might need to install different tools like Node, Java, .Net etc... to get different part of a distributed system up. With docker we could run for instance java applications with out having java in the host machine. This drastically reduces the time to set up local environment.

## Docker reduces the communications and co-ordination needed between dev and ops team:
 When a development team develops an application, and shares it with deployment team, typically they would shares couple of binaries as zip file. It would also be necessary to share information about dependencies and the installation procedure. With docker these things are simplified by providing a registry to share docker images instead of binaries. Also the command to get the system is made uniform and simpler.
 
## Docker provides a high degree of isolation between different applications:
 When we develop distributed systems, there are many applications and each application needs a different kind of server for deployment. This increases the number of servers. With docker, many containers that have different system requirments could be run on the same physical server or Virtual machine. This reduces the cost of the insfrastructure.
 
## Ecosystem has drastically evolved for container based development:
The ecosystem for developing, monitoring, deploying container (docker) based application has drastically evolved. There are several hundreds of popular tools that could help in the development process. Few examples would be docker-compose, docker swarm, kubernetes, helm, open shift. There are also offerings from cloud providers like Azure, AWS and GCP to deploy docker images.