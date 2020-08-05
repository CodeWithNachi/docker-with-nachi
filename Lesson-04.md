# Lesson 04

## Intention
 * Understand the docker networking basics
 * Understand exposing a port to the host machine
 * Accessing the docker from host
 * Accessing the host from docker
 * Accessing one docker from another

# Experiment 1
 * Lets run the command `docker run -d --name mymodnginx modified-nginx`
 * Now the container is running and it can serve the web page, but we can not access it from the host system
 * We can verify this by the command `docker exec mymodnginx curl http://localhost:80`. This will run curl from within the container
 * We can access this page from the host machine

# Experiment 2
 * Now lets run another container from the same image this time with publishing the containers port
 * Running the command `docker run -d --name mymodnginx-new --publish 8090:80 modified-nginx` we can see the page by at the end point http://localhost:8090
 * We could also run the shorter verision of the command `docker run -d --name mymodnginx-new -p 8090:80 modified-nginx`
 * We have now seen how to access a service running in docker from host machine. Now lets see how to access a host service from docker

# Experiment 3
 * To simulate running a service in the host machine let's run the command `docker run --name local -d -p 8090:80 nginx`
 * Let now create a new docker container and access the service running is 8090
 * Let's create a container by the command `docker run --name mynginx -d nginx`
 * The host machine is accessible in the URI host.docker.internal
 * Let run the command `docker exec mynginx curl host.docker.internal:8090`
 * By the output of the above command we know that we can reach host service from a docker container 

# Experiment 4
 * Docker containers can communicate with each other by the names
 * We can create a network in docker.
 * A docker container can be part of many networks.
 * A docker container can communicate with the other using the name. Let's try this out by the below command
   * `docker network create -d bridge mynet`
   * `docker run --name container1 -d --network mynet nginx`
   * `docker run --name container2 -d --network mynet nginx`
   * `docker exec container1 curl container2`
 
 # Experiment 5
 * Now lets run the same experiment without specifing the network
   * `docker run --name container1 -d nginx`
   * `docker run --name container2 -d nginx`
   * `docker exec container1 curl container2`
 * The output should indicate the containers are not able to communicate with each other
 * When no network is specified docker associates the container in the default bridge network. The default bridge network does not support name resolution.
 * However communication is possible through IP without name resolution
 
 # Experiment 5
 * Lets try to communicate through IP address
 * The IP address of a container named container2 could be got through the command `docker inspect container2`
 * The above command gives a lot of information, we can filter only the IP by adding a format as shown below
 * `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container2`
 * Now we should be able access service in container2 from container1 by `docker exec container1 curl <container2-ip>`
 
 # Experiment 6
 * 
# Summary
 * Any changes to the container will be lost when the container is removed
 * Containers can be created out of a image by docker run or docker create commands
 * Image can be created out a container by docker commit command

# Test youself
 * Create a container from nginx image
 * Add a page to the nginx container
 * Create an image from the nginx container
 * Verify if the added page is there in the image by spinning up a new container

