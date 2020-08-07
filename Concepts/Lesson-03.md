---
sort: 3
---
# Container changes are short lived

## Intention
 * Understand the changes to container are not going to affect the image
 * How to create a image out of a container
 * Ways to copy files in and out of container

# Experiment 1
 * Lets run a nginx container with the below command
```bash
docker run -p 8090:80 -d --name mynginx nginx
```
 * Lets run the below command to list the contents of the directory `/usr/share/nginx/html`
```bash
docker exec -it mynginx -w /usr/share/nginx/html mynginx ls
```
 
# Experiment 2
 * From a command prompt, in a directory where we have write permission, lets run below command to copy index.html to host machine
```bash
docker cp mynginx:/usr/share/nginx/html/index.html ./mypage.html
```
 * This command should copy the file /usr/share/nginx/html/index.html from the container to your local directory as mypage.html.

# Experiment 3
 * In the host machine in the file mypage.html let us Replace "Welcome to nginx" with "Welcome to my page" with any text editor of our choice
 * Now lets run the below command to copy the modified file mypage.html
```bash
docker cp ./mypage.html mynginx:/usr/share/nginx/html/mypage.html
```
 * Lets view the page [http://localhost:8090/mypage.html](http://localhost:8090/mypage.html) in incognito mode to verify if the modified page is available

# Experiment 4
 * Now let us stop this container and run from the image
 * To stop and remove the container run the command `docker stop mynginx && docker rm mynginx`
 * Now lets run the container again by the command `docker run -p 8090:80 -d --name mynginx nginx`
 * When we go to the page http://localhost:8090/mypage.html, we are greeted with a page not message (Make sure you in incognito mode to avoid caching)
 * From this experiment we can understand that any change in the container is not written to the image what was used to spin up the container
 * Any change is the container will be lost once the container is removed
 
# Experiment 5
 * Now let us add the new page in the new container by the command `docker cp ./mypage.html mynginx:/usr/share/nginx/html/mypage.html`
 * Now we should be able access the new page http://localhost:8090/mypage.html
 * We can create an image named mod-nginx from the container by the command `docker container mynginx mod-nginx`
 * We can stop and remove the current container with the command `docker stop mynginx && docker rm mynginx`
 * We can create a new container from the modifined image by the command `docker run -p 8090:80 -d --name mod-nginx nginx`
 * We can verify that container is able to serve the page http://localhost:8090/mypage.html

# Experiment 6
 * TBD Creating an image out of the contianer

# Experiment 7
 * Running another container

# Summary
 * Any changes to the container will be lost when the container is removed
 * Containers can be created out of a image by docker run or docker create commands
 * Image can be created out a container by docker commit command

# Test youself
 * Create a container from nginx image
 * Add a page to the nginx container
 * Create an image from the nginx container
 * Verify if the added page is there in the image by spinning up a new container

