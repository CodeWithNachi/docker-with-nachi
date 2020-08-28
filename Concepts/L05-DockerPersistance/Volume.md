---
sort: 1
---

# Volume --> Persitent Data



## What we will see here
* Creation of volume which is outside the container aka as Named Volumes
* Volume outlive the containers and has to be deleted manually

# Experiment 1
 * Lets start a nginx container which creates a new volume
 * Here we will populates the new volume nginx-vol with the contents of the container’s /usr/share/nginx/html directory, which is where Nginx stores its default HTML content
```bash
docker  run -d --name mynginx -v nginx-vol:/usr/share/nginx/html nginx
```
# Experiment 2
 * Now we will do an inspect and check if the location of the mounts, which in any case should always be a unique location on the host machine.
```bash
docker  inspect mynginx
```
 * The output will be as shown below in the picture.
 ![viewing my page](/L05-E01-P01.PNG)
# Experiment 3
 * Now we check if the volume which we created is existing or not
```bash
docker volume ls
```
 * The output will be as shown below in the picture.
 ![viewing my page](/L05-E01-P02.PNG)
# Experiment 4 
 * Now we will remove the container and see if the volume still persist
```bash
docker rm -f mynginx
```
 * now if we check the volume, we should still be able to see the volume
```bash
docker volume ls
```
# Experiment 5
 * Now lets try to run a new nginx container and attach this existing Volume to it
 * In order to do that the name of the volume has to be same
 * run a new container named as mynginx2
```bash
docker  run -d --name mynginx2 -v nginx-vol:/usr/share/nginx/html nginx
```
# Experiment 6
 * Now if we check which if its using the same volume or not
```bash
docker  inspect mynginx2
```
 * The output will be as shown below in the picture.
 ![viewing my page](/L05-E01-P03.PNG)

# Experiment 7
 * In order to delete the container and volume we need to explicitly delete both. 
 * We need to ensure that the container which is using the volume has to be deleted first
```bash
docker rm -f mynginx2
```
```bash
docker volume rm nginx-vol
```
# Experiment 8
 * Now we would see that the volume can actually contain data inside it, let create one 
```bash
docker  run -d --name mynginx -p 8090:80 -v nginx-vol:/usr/share/nginx/html/data nginx
```
 * Now lets try to copy the index file to a different folder in the Volume
```bash
docker exec -w /usr/share/nginx/html mynginx cp ./index.html ./data/index.html
```
 * Lets try to access the index.html file from the new location, which is from the data folder
 * The output will be as shown below in the picture.
 ![viewing my page](/L05-E01-P04.PNG)
 
# Summary
 * Names volumes are user friendly and let the user know for what that volume was created
 * Volume has to be deleted manually( Database will outlived the executable)
 * Volume can contains data
 * Volume can be used to share data across containers
 
# Test youself
 * Database upgrade with containers
 * Create a mysql container with named volume **mysql-db** using version 5.7
 * Use Docker hub to learn Volume path and versions needed to run it
 * Check logs, stop container
 * Create a new mysql container with the same named volume using version 8.0
 * Check logs to validate


