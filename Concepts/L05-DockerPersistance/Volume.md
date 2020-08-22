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
* This is not so user friendly as it don't tell us which container this volume is assigned to
```bash
docker volume ls
```
* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P02.png)

# Experiment 4 
* Now we will remove the container and see if the volume still persist
```bash
docker container rm mysql
```
* now if we check the volume, we should still be able to see the volume

```bash
docker volume ls
```
# Experiment 5
* To make Volume user friendly, we can create Named Volumes
* -v : allows us to specify either a new volume that we want to create for this container
```bash
docker  run -d --name mysql2 -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql
```

# Experiment 6
* Now if you do a inspect of this runnig container, you would see 

```bash
docker volume inspect mysql-db
```

* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P04.png)

# Experiment 7
* Now if we delete this container and run another container and attach this volume
```bash
docker rm -f mysql2
```
* run a new container named as mysql3
```bash
docker  run -d --name mysql3 -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql
```
# Experiment 8
* Now if we check which if its using the same volume or not
```bash
docker  inspect mysql3
```
* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P05.png)

# Summary
 * Need to check the docker file of a container if you need to worry about volumes
 * Volume has to be deleted manually( Database will outlived the executable) 
 * Names volumes are user friendly and let the user know for what that volume was created


# Test youself
 * Database upgrade with containers
 * Create a mysql container with named volume *mysql-db* using version 5.7
 * Use Docker hub to learn Volume path and versions needed to run it
 * Check logs, stop container
 * Create a new mysql container with the same named volume using version 8.0
 * Check logs to validate


