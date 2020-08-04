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
 * When we go to the page http://localhost:8090/mypage.html
 

 
# Experiment 11
 * Stop and restart the image
 
# Experiment 12
 * commiting and starting a container
 

# Experiment 04
 * Spin up a new container
 * File is lost
 * Add the file
 * Image is not modified
 
# Experiment 05
 * Create an image
 * stop the contianer and start another one
 
# Experiment 06
 * Copy files in to the container

# Experiment 07
 * Copy files out of the container

# Experiment 08
 * uname -r
 * docker run -it --rm -p 8888:8080 tomcat:9.0

