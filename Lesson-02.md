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
 * Lets run the command `docker exec -w /usr/share/nginx/html mynginx sh -c 'echo "hello" > ./mypage.html'`. This creates a file name mypage.html in the directory `/usr/share/nginx/html` with the content hello 
 * By running the command `docker exec -w /usr/share/nginx/html mynginx ls`, we can verify the file is created 
 * When we hit the end point http://localhost:8090/mypage.html, we can see that our newly created file is also server by nginx
 * From the experiment, it looks like docker container has a file system that we can also modify

# Experiment 04 (Getting in to the docker container shell)
 * Till now we were running commands from the host machines and some other command got executed in the docker container.
 * Now lets run the command `docker exec -w /usr/share/nginx/html -it mynginx /bin/bash`. This opens a bash shell for us to interact with the docker.
 * On running the command, we can see that prompt has changed.
 * Now we can now execute command in the bash shell directly.
 * Let verify by running the command `ls`
 
# Experiment 05 (Running command in docker container shell)
 * Let's run the linux command that prints the linux distribution `cat /etc/os-release`.
 * It looks like this docker is not just a file system but also an debian OS
 
# Experiment 06 (Running command in docker container shell)  
 * Now lets run the command to list the processes `ps aux`. But on running the command, we realize that ps is not available.
 * As this docker container seems to be a Debian Linux OS, lets try to install procps by the command `apt update && apt install -y procps`
 * From the logs it would be clear that we have installed procps successfully in the docker container
 * We can verify the procps is correctly installed by running the command `ps aux`
 * From the experiment 
   * It feels like docker is like a virtual machine 
   * It has its own operating system
   * It has its own file system
   * It runs it's own processes (However it seems to running lesser number of processes compared to a VM, and also the UI that is there in the VM is not there)
   
# Experiment 07 (Running command in docker container shell)
 * Now lets run the linux command to display the kernel information `uname -r`
 * Running this command we see the kernel information of the docker.
 * Now that we have played around enough, lets go back to the host prompt by the command `exit`.
 * At this point docker containers look like a machine running an OS and we can run commands on it or we can interact with it by opening a terminal
 
# Experiment 08 
 * Lets play around with another popluar container tom cat, we can get the container up by the command `docker run -d --name mytomcat tomcat:9.0`
 
 
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

 
