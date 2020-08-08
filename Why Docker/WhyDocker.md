# Why Docker

Before learning the concepts of docker. Let understand the advantages of docker.

## Installation/Unistallation of applications is easy and secure:
 For a docker user, installing and uninstalling applications such as MongoDB, PostgreSQL, RabbitMQ, Kafka, RedisCache, Keycloak are extraordinarily easy. The applications could in installed and uninstalled in a single command. When running the applicaitons as a docker container it gives a very good degree or isolation. The docker containers don't interfer with the system files making it much more secure.  
 
 This could be very useful for developers as there is a constant need to install and unistall softwares for experimenting purposes.
 
## Sharing/Publishing/Packagin of application is made simpler: 
 When an application is developed there are dependencies it has on the operating system it is going to run on. When we package the application as a docker image, we are also packaging the operating system in it. This makes it easy for sharing applications. So when we run docker containers we don't need to worry about the operating system requirments.

## Simplifies local developement setup
 When organization develop system. Different components are often developed in different languages. So one developer might need to install different tools like Node, Java, .Net etc... to get different part of a distributed system up. With docker we could ran for instance java applications with out having java in the host machine. This drastically reduces the time to set up local environment

## Docker reduces the communications and co-ordination needed between dev and ops team:

 * Docker provides a high degree of isolation between different applications:
 * Orchestration tools like kubernetes, docker swarm that are build around containers (docker) make it easy to manage huge number of applications.