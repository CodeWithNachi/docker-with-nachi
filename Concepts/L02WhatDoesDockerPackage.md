---
sort: 3
---
# What Does Docker Package

## What we will see
 * We'll see docker packages not only the application
 * It nearly packages the entire operating system
 * It leaves out the kernel (which contains the scheduler) while packaging. All docker containers will will use host kernel. 

## Experiment 01
 * Lets create a container to do this experiment with the command below
```bash
docker run --name mynginx -d -p 8090:90 nginx
```
 * Now we can execute the linux command `ls` inside the container in a directory `/usr/share/nginx/html` by running the below docker command
```bash
docker exec -w /usr/share/nginx/html mynginx ls
```
 * The output of the above should look like the image below indicating there are 2 files named 50x.html and index.html in the directory `/usr/share/nginx/html`
![viewing the filesystem inside docker](/L02-E01-P01.png) 
 * Now we have seen that docker is not only packaging the application. It can have files as well packaged in it.

## Experiment 02
 * In the previous experiment we listed the files in a directory.
 * Now to see the content of the file index.html, by running the below command
```bash
docker exec -w /usr/share/nginx/html mynginx cat index.html
```
 * The output is as shown below. If we browse the page [http://localhost:8090](http://localhost:8090), we can observe the index files is what is getting server in the page
![viewing the contents of a file](/L02-E02-P01.png) 
 
## Experiment 03
 * Lets not create a file inside the container with the content `hello` named `mypage.html` with the command below
 * If you are running commands in bash
```bash
docker exec -w /usr/share/nginx/html mynginx sh -c 'echo "hello" > ./mypage.html'
```
 * If you are running commands in windows command prompt
```bash
docker exec -w /usr/share/nginx/html mynginx sh -c "echo hello > ./mypage.html"
```
 * We can veify the file is created by the below command, and the output should look something like below picture
```bash
docker exec -w /usr/share/nginx/html mynginx ls
```
![listing the newly created file](/L02-E03-P01.png) 
 * When we browse the page in incognito mode [http://localhost:8090/mypage.html](http://localhost:8090/mypage.html), we can observer that our newly created file is also server by nginx as a page. After all, this is something that we could expect from a nginx application
 * From the experiment, it looks like docker container has a file system that we can also modify

## Experiment 04 (Moving to docker container prompt)
 * Till now we were running docker commands that executed related linux command in the container. Now lets open a interactive shell of the container with the command below
```bash
docker exec -w /usr/share/nginx/html -it mynginx /bin/bash
```
 * On running the above command, we should observe that the prompt has change. This is an interactive shell of the docker container.
 * We can run commands directly in the container now. Let's run `ls` command to see the list of files
```bash
ls
```
 
## Experiment 05 (Inside the docker container prompt)
 * Let's run the below linux command that prints the linux distribution details
```bash
cat /etc/os-release
```
 * The ouptut should be like the image below. It looks like this docker container is not just a file system but also has an debian OS
 
## Experiment 06 (Inside the docker container prompt)  
 * Now lets run the below command to list the processes in linux
```bash
ps aux
```
 * Running the above we should get an output as shown below indicating the command is not available.
 * As this docker container seems to be a Debian Linux OS, lets try to install procps by the below command
```bash
apt update && apt install -y procps
```
 * The output should be similar to the below image. And it would indicate procps is installed
 * We can verify the procps is correctly installed by running the below command
```bash
ps aux
```
 * The output should look something like below. Listing all the processes that are running
 * From the experiment 
   * It feels like docker is like a virtual machine 
   * It has its own operating system
   * It has its own file system
   * We can install software in it, and probably uninstall software from it
   * It runs it's own processes (However it seems to running lesser number of processes compared to a VM, and also the UI that is there in the VM is not there)
   
## Experiment 07 (Inside the docker container prompt)
 * Now lets run the below linux command to display the kernel information
```bash
uname -r
```
 * The output should be as shown below
 * Now that we have played around enough, lets go back to the host prompt by the below command
```bash
exit
```
 * At this point docker containers look like a virutal machine running an OS and we can run commands on it or we can interact with it by opening a terminal
 * However it didn't run many processes like a virtual machine would. Also it didn't provide us an UI that could be provided by VMs
 * Now lets stop and remove the container. We are used to doing this in two command, but we could do it just the rm command with a flag as shown below
```bash
docker rm -f mynginx
```
 
## Experiment 08 
 * Lets now play around with an image that has nginx installed on top a alpine distro. Lets run the container by the below command.
```bash
docker run --name alpine-nginx -d nginx:1.19.1-alpine
```
 * We have now started an another container named alpine-nginx.
 * To the know the OS used in this container lets run the below command
```bash
docker exec alpine-nginx cat /etc/os-release
```
 * The output should look showthing like its shown in the image below. And we can observe that we are running Alpine Linux
 
## Experiment 09
 * Now lets print the kernel information by the below command 
```bash
docker exec alpine-nginx uname -r
```
 * The output should be as shown in below. 
 * We can observe the first container and second container though they are using different OS are using the same kernel
 * This experiment helps us understand the following
   * Each docker container can have its own operation system
   * Each docker container can have its own file system
   * They seem to using the same kernel or sharing the kernel
 * Docker containers do not have their own kernel. They use the host system's kernel. By doing so, dockers are much more leaner then VMs
 * They are also generally tweaked to do one thing and that one thing well. So all the unnecessary proccess and files are generally striped off.
 * Docker does not provide a way for the container to have a UI. However UI processes could be run (if we need) in the container and we could connect using a remote desktop softare.
 * Lets now remove the container with below command
```bash
docker rm -f mynginx
```

## Summary
From the experiments conducted till now we can understand the following
 * Container is something like a Virtual machine.
 * Each container has a file system, and can run processes in it.
 * Unline a VM, a container does not have it's own kernel (scheduler). It shares the kernel with the host machine.
 * Containers are leaner than virtual machines
   * Containers has lesser number of files in the file system compared to VMs
   * Containers has lesser number of processes running in it compared to VMs
   * Containers has lesser softwares installed in it compared to VMs
 * Generally the practice is to create an image that can do one job, and only softwares needed to do that job is installed.

# Test your self
 * Run a container from nginx image
 * Add a new page to the nginx container
 * Find the linux distro that the nginx container is runnning
 * Install procps in the container and list the running processes


 
