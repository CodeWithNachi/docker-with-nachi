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
 * The host machine is accessible in the URI docker.host.internal
 * Let run the command `docker exec mynginx curl docker.host.internal:8090`
 
 
# Experiment 3
 * Lets run command `docker cp mynginx:/usr/share/nginx/html/index.html ./index.html`
 * This command should copy the file /usr/share/nginx/html/index.html from the container to your local directory from where you are running your command
 * In the host machine, let us Replace "Welcome to nginx" with "Welcome to my page" in the local machine using any standard text editor
 * Now lets run the command `docker cp ./index.html mynginx:/usr/share/nginx/html/mypage.html` to copy the modified index.html as mypage.html
 * Lets verify if the modified content is available in http://localhost:8090/mypage.html

# Experiment 4
 * Now let us stop this container and run from the image
 * To stop and remove the container run the command `docker stop mynginx && docker rm mynginx`
 * Now lets run the container again by the command `docker run -p 8090:80 -d --name mynginx nginx`
 * When we go to the page http://localhost:8090/mypage.html, we are greeted with a page not message (Make sure you in incognito mode to avoid caching)
 * From this experiment we can understand that any change in the container is not written to the image what was used to spin up the container
 * Any change is the container will be lost once the container is removed
 
# Experiment 5
 * Now let us add the new page in the new container by the command `docker cp ./index.html mynginx:/usr/share/nginx/html/mypage.html`
 * Now we should be able access the new page http://localhost:8090/mypage.html
 * We can create an image named mod-nginx from the container by the command `docker container mynginx mod-nginx`
 * We can stop and remove the current container with the command `docker stop mynginx && docker rm mynginx`
 * We can create a new container from the modifined image by the command `docker run -p 8090:80 -d --name mod-nginx nginx`
 * We can verify that container is able to serve the page http://localhost:8090/mypage.html

# Summary
 * Any changes to the container will be lost when the container is removed
 * Containers can be created out of a image by docker run or docker create commands
 * Image can be created out a container by docker commit command

# Test youself
 * Create a container from nginx image
 * Add a page to the nginx container
 * Create an image from the nginx container
 * Verify if the added page is there in the image by spinning up a new container

