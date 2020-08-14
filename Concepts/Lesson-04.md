---
sort: 5
---
# Docker networking

## Intention
 * Understand the docker networking basics
 * Understand exposing a port to the host machine (publish)
 * Accessing the docker from host
 * Accessing the host from docker
 * Accessing one docker from another

## Experiment 1
 * Prerequisite: Creation of modified-nginx image as seen in the previous lesson
 * Lets run the command below to run the modified nginx
```bash
docker run -d --name mymodnginx modified-nginx
```
 * Now the container is running and it can serve the web page, but we can not access it from the host system
 * We can verify this by the below command. This will run curl from within the container
```bash
docker exec mymodnginx curl http://localhost:80
```

## Experiment 2
 * Now lets run another container from the same image this time with publishing the containers port
 * Running the below command and we can see the page by at the end point http://localhost:8090
```bash
docker run -d --name mymodnginx-new --publish 8090:80 modified-nginx
```
 * We could also run the shorter verision of the command `docker run -d --name mymodnginx-new -p 8090:80 modified-nginx`
 * We have now seen how to access a service running in docker from host machine. Now lets see how to access a host service from docker

## Experiment 3
 * To simulate running a service in the host machine let's run the command below
```bash
docker run --name local -d -p 8090:80 nginx
```
 * Let now create a new docker container and access the service running is 8090
 * Let's create a container by the command 
```bash
docker run --name mynginx -d nginx
```
 * The host machine is accessible in the URI `host.docker.internal`
 * Let run the command belwo to verify it
```bash
docker exec mynginx curl host.docker.internal:8090
```
 * By the output of the above command we know that we can reach host service from a docker container 

## Experiment 4
 * Docker containers can communicate with each other by the names
 * We can create a network in docker.
 * A docker container can be part of many networks.
 * A docker container can communicate with the other using the name. Let's try this out by the below command
```bash
docker network create -d bridge mynet
```
```bash
docker run --name container1 -d --network mynet nginx
```
```bash
docker run --name container2 -d --network mynet nginx
```
```bash
docker exec container1 curl container2
```
 
 ## Experiment 5
 * Now lets run the same experiment without specifing the network
   * `docker run --name container1 -d nginx`
   * `docker run --name container2 -d nginx`
   * `docker exec container1 curl container2`
 * The output should indicate the containers are not able to communicate with each other
 * When no network is specified docker associates the container in the default bridge network. The default bridge network does not support name resolution.
 * However communication is possible through IP without name resolution
 
 ## Experiment 6
 * Lets try to communicate through IP address
 * The IP address of a container named container2 could be got through the command `docker inspect container2`
 * The above command gives a lot of information, we can filter only the IP by adding a format as shown below
 * `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container2`
 * Now we should be able access service in container2 from container1 by `docker exec container1 curl <container2-ip>`
 
 ## Experiment 7
 * Lets try to communicate between docker containers running in different networks by the below commands
 * `docker network create net1`
 * `docker network create net2`
 * `docker run --name web1 --network net1 -d nginx`
 * `docker run --name web2 --network net2 -d nginx`
 * We can verify that web2 is not reachable from container web1 by the running the command `docker exec web1 curl web1`
 * We can repeat the experiment by specifying the ip address instead of the name. The command for getting the IP address is below
 * `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web2`
 * Command to attempt access of web2 is docker exec web1 curl <ip-address of web2>
 
 ## Experiment 8
 * Now we could connect the container web2 to net1 and we can verify connectivity between web1 and web2
 * To connect web2 and net1 run the command `docker network connect net1 web2`
 * Now we should be able access web2 home page from web1 by `docker exec web1 curl web2`
 
# Summary
 * We can publish the docker container port using --publish or -p option
 * The docker containers can access the service running on the host with the uri host.docker.internal
 * Containers running in the same network can resolve other containers name to an ip address
 * When creating a container we could specify a network. when not specified the container is associated with the default bridge network
 * default bridge network does not offer dns resolution of name
 * One docker can be in multiple networks
 * In this section we have created networks using bridge driver. Other drivers are not covered as a part of this lesson.

# Test youself
 * Create a container from nginx image and access that web page locally by publishing
 * Access a service running in host machine (or simulated to be running in your host) from a docker container
 * Access a service running in one docker container from another by making them in the same network
 * Access a service running in one docker container from another by making them in the default network. Also show dns resolution is not possible
 * Verify that two dockers associated with different networks can not communicate
