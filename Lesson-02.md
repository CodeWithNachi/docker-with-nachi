# Lesson 02

## Intention
 * Understand the similarity and differences between Docker Containers and Virtual machines
 * Run commands in containers
 * Copy contents to and from containers

# Experiment 01
 * Run the following commands
   * `docker run --name mynginx -d -8090:80 nginx`
   * `docker exec -w /usr/share/nginx/html mynginx ls` . This command executes a command `ls` in the container named mynginx in the directory `/usr/share/nginx/html`
 * From the above command output, we know that there are 2 files (50x.html and index.html) in the directory `/usr/share/nginx/html`
 * After this experiment, docker container looks more than an application, it has directories and seems to have files in it.

# Experiment 02
 * In the previous experiment we listed the files.
 * Now to see the content of the file index.html, by running the command `docker exec -w /usr/share/nginx/html mynginx cat index.html`
 * We can realize that the content of index.html is what is servered in the endpoint http://localhost:8090
 
# Experiment 03
 * Let us create new file named mypage.html in the directory `/usr/share/nginx/html` with the content "hello" by the command `docker exec -w /usr/share/nginx/html mynginx sh -c 'echo "hello" > ./mypage.html'`
 * Now we can verify if the file is created by listing the contents of the directory with the command `docker exec -w /usr/share/nginx/html mynginx ls`
 * When we hit the end point http://localhost:8090/mypage.html, we can see that our newly created file is also server by nginx

# Experiment 03
 * docker exec -w /usr/share/nginx/html mynginx -it /bin/bash
 * cat /etc/os-release
 * apt update
 * apt install -y procps
 * ps aux
 
 
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

 
