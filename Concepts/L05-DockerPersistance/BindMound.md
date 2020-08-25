---
sort: 2
---

# Bind Mount

## What we will see here
* Maps a host file or directory to a container file or directory

# Experiment 1
 * Lets start a nginx container mapping a new html file.
 * Lets create a index.html file with text "Nginx: Showing result from Host Machine and not from the Container"Nginx: Showing result from Host Machine and not from the Container
 * Since I have created the file from the default location my powershell is running, I will use the $(pwd) command to get the path
```bash
docker run -d --name mynginx -p 8090:80 -v ${PWD}:/usr/share/nginx/html nginx
```
 * The output will be as shown below in the picture.
 ![viewing my page](/L06-E01-P01.PNG)
