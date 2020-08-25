---
sort: 2
---

# Bind Mount

## What we will see here
* Maps a host file or directory to a container file or directory

# Experiment 1
 * Lets start a nginx container mapping a new html file.
 * Lets create a index.html file with text "Nginx: Showing result from Host Machine and not from the Container"Nginx: Showing result from Host Machine and not from the Container
 * Since I have created the file from the default location my powershell is running, I will use the ${PWD} command to get the path in windows ( for Linux the command would be $(pwd))
```bash
docker run -d --name mynginx -p 8090:80 -v ${PWD}:/usr/share/nginx/html nginx
```
 * The output will be as shown below in the picture.
 ![viewing my page](/L06-E01-P01.PNG)


# Experiment 2
 * Now we will check if Nginx is picking file from the host machine
 * In order to do so, let get inside the container
 ```bash
docker exec -it mynginx bash
```
* Now we will go to the location which we mounted using the below command inside the bash
 ```bash
cd /usr/share/nginx/html
```
* if we do an ls ( List all the files), it will show the content of our local directory
 ```bash
ls
```
 * The output shown as below( depending on what you have in the current folder)
 ![viewing my page](/L06-E01-P02.PNG)
 
 # Summary
 * Mounting a file/dir in the container( Deleting them in the container would delete them on the host machine)
 * Mount is ideal for developers, since they dont have to dockerize anything while they are still developing & can see the changes quickly.
 


 
