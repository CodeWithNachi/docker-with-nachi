# Lesson 02

## Intention
 * Understand the similarity and differences between Docker Containers and Virtual machines
 * Run commands in containers
 * Copy contents to and from containers

# Experiment 01
 * Run the following commands
   * `docker run --name mynginx -d -p 8090:80 nginx`
   * `docker exec -w /usr/share/nginx/html mynginx ls` . This executes the command `ls` in the container named mynginx in the directory `/usr/share/nginx/html`
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
 * From the experiment, it looks like docker container has a file system that we can also modify

# Experiment 04
 * Till now we were running commands from the host machine that get executed in docker container
 * Now lets run the command `docker exec -w /usr/share/nginx/html -it mynginx /bin/bash`. This opens a bash shell for us to interact with the docker.
 * we can now execute command in the bash shell directly without prefixing `docker....`
 * Let's run the linux command that prints the linux distribution `cat /etc/os-release`.
 * Running the above command, it looks like docker is not just a file system but also an OS. In this case a debian
 * Now lets run the command `ps aux`. This command is used to list the processes that are running in linux. But on running the command, we realize that ps is not available.
 * As this docker container seems to be a Debian Linux OS, lets try to install procps by the command `apt update && apt install -y procps`
 * Running the above command, it looks like we can also install softwares in docker containers.
 * Now let's run the command to list the processes `ps aux` in the docker shell
 * Running the above command, we realize few processes are only running
 * From the experiment it feels like docker is like a virtual machine that can have its own operating system, file system and runs it's own processes. However it doesn't seem to have a UI.
 
 
 
 
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

 
