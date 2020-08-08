# Why Docker

Before learning the concepts of docker. Let understand the advantages of docker.

## Installation/Unistallation of applications is easy and secure:
 For a docker user, installing and uninstalling applications such as MongoDB, PostgreSQL, RabbitMQ, Kafka, RedisCache, Keycloak are extraordinarily easy. The applications could in installed and uninstalled in a single command. When running the applicaitons as a docker container it gives a very good degree or isolation. The docker containers don't interfer with the system files making it much more secure.  
 
 This could be very useful for developers as there is a constant need to install and unistall softwares for experimenting purposes.
 
## Sharing/Publishing/Packagin of application is made simpler: 
 When an application is developed there are dependencies it has on the operating system it is going to run on. When we package the application as a docker image, we are also packaging the operating system in it. This makes it easy for sharing applications. So when we run docker containers we don't need to worry about the operating system requirments.

## Simplifies local developement setup:
 When organization develop system. Different components are often developed in different languages. So one developer might need to install different tools like Node, Java, .Net etc... to get different part of a distributed system up. With docker we could ran for instance java applications with out having java in the host machine. This drastically reduces the time to set up local environment

## Docker reduces the communications and co-ordination needed between dev and ops team:
 When a development team develops and applicaiton, and shares it with deployment team, typically they would shares couple of binaries as zip file. It would also be necessary to share information about dependencies and the installation procedure. With docker these things are simplified by providing a registry to share docker images instead of binaries. Also the command to get the system is made uniform and simpler.
 
## Docker provides a high degree of isolation between different applications:
 When we develop distributed systems, there are many applications and each application needs a different kind of server for deployment. This increases the number of servers. With docker many containers that have different system requirments could be run on the same phyical server or Virtual machine. This reduces the cost of the insfrastructure
 
## Ecosytem has drastically evolved for container based developement:
The ecosystem for developing, monitoring, deploying container (docker) based application has drastically evolved. There are several hundereds of popular tools that could help in the development process. Few examples would be docker-compose, docker swarm, kubernetes, helm, open shift. There are also offerings from cloud providers like Azure, AWS and GCP to deploy docker images.

 