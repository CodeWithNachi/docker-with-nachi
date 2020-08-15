---
sort: 4
---
# Changes To Container Are Not Persisted

## What we will see
 * Understand the changes to container are not going to affect the image
 * How to create an image out of a container
 * Ways to copy files in and out of container

# Experiment 1
 * Lets run an nginx container with the below command
```bash
docker run -p 8090:80 -d --name mynginx nginx
```
 * Lets run the below command to list the contents of the directory `/usr/share/nginx/html`
```bash
docker exec -it -w /usr/share/nginx/html mynginx ls
```
 
# Experiment 2
 * From a command prompt, in a directory where we have written permission, lets run the below command to copy index.html to host machine
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
 * We are going to stop and remove the running container, and then spin up a new container from the image
 * First lets stop and remove the container by the below command
```bash
docker rm -f mynginx
```
 * Now lets spin up another container by the below command
```bash
docker run -p 8090:80 -d --name mynginx nginx
```
 * On visiting the page [http://localhost:8090/mypage.html](http://localhost:8090/mypage.html), in incognito mode we will observe that the page is not found.
 * From this experiment we can understand that any change in the container is not written to the image what was used to spin up the container
 * Any change in the container will be lost once the container is removed
 
# Experiment 5
 * Now let us add the new page in the new container by the below command 
```bash
docker cp ./mypage.html mynginx:/usr/share/nginx/html/mypage.html
```
 * We should be able to view the page [http://localhost:8090/mypage.html](http://localhost:8090/mypage.html) in incognito mode.
 * We can create an image named `mod-nginx` from the container by the below command 
```bash
docker container mynginx mod-nginx
```
 * We can stop and remove the current container with the below command 
```bash
docker rm -f mynginx
```

# Experiment 6
 * We can create a new container from the modified image by the command below. We are not creating from the default nginx image. But from mod-nginx image
```bash
docker run -p 8090:80 -d --name mod-nginx nginx
```
 * In this container we can see that page we added is available by visiting [http://localhost:8090/mypage.html](http://localhost:8090/mypage.html)
 * We can stop and remove the current container with the below command 
```bash
docker rm -f mynginx
```

# Summary
 * Any changes to the container will be lost when the container is removed
 * Containers can be created out of a image by docker run or docker create commands
 * Image can be created out a container by docker commit command

# Test youself
 * Create a container from nginx image
 * Add a page to the nginx container
 * Create an image from the nginx container
 * Verify if the added page is there in the image by spinning up a new container

