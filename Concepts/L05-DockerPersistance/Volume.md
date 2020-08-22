---
sort: 1
---

# Volume --> Persitent Data

* In order to check if we need to worry about using a volume we need to have a look at the docker file of a container. Go to [Docker Hub] (hub.docker.com) and check the docker file of any container. I am using MYSQL as an example as details would always have volume

![viewing my page](/L05-E01-P03.png)

## What we will see here
* Creation of volume which is outside the container 
* Volume outlive the containers and has to be deleted manually

# Experiment 1
 * Lets run an mysql container with the below command
```bash
docker  run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
```
# Experiment 2
* Now we will do an inspect and check if the location of the mounts, which in any case should always be a unique location on the host machine.
```bash
docker  inspect mysql
```
* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P01.png)
# Experiment 3
* Now we check if the volume which we created is existing or not
```bash
docker volume ls
```
* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P02.png)

# Experiment 4 
* Now we will run another mysql container and chek 

# Summary
 * Need to check the docker file of a container if you need to worry about volumes
 * Volume has to be deleted manually( Database will outlived the executable) 


# Test youself
 * Check if need a Volume for PostGres container


