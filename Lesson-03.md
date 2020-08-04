# Lesson 03

## Intention
 * Understand the changes to container are not going to affect the image
 * How to create a image out of a container
 * Ways to copy files in and out of container

# Experiment 1
 * Lets run a nginx container with the command `docker run -p 8090:80 -d --name mynginx nginx`
 * Lets run the command `docker exec -it mynginx -w /usr/share/nginx/html mynginx`. This command will tell the contents of the directory /usr/share/nginx/html
 
# Experiment 2
 * Lets run command `docker cp mynginx:/usr/share/nginx/html/index.html ./index.html`
 * This command should copy the file /usr/share/nginx/html/index.html from the container to your local directory from where you are running your command

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
 

