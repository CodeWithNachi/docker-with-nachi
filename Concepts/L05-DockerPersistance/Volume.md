---
sort: 1
---

# Volume --> Persitent Data

* In order to check if we need to worry about using a volume we need to have a look at the docker file of a container. Go to hub.docker.com and check the docker file of any container. I am using MYSQL as an example as details would always have volume

![viewing my page](/L05-E01-P03.png)

## What we will see here
* Creation of volume which is outside the container 
* Volume outlive the containers and has to be deleted manually

# Experiment 1
 * Lets run an mysql container with the below command
```bash
docker  run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
```
```bash
docker  inspect mysql
```
* Now if you do a docker inspect you should be able to  the below output under mounts which will show a unique location under host to store the date
* The output will be as shown below in the picture.
![viewing my page](/L05-E01-P01.png)

```bash
docker volume ls
```
* Now if we do a volume ls it will show a volume automatically created
![viewing my page](/L05-E01-P02.png)



# Summary
 * Need to check the docker file of a container if you need to worry about volumes
 * Volume has to be deleted manually


# Test youself
 * Check if need a Volume for PostGres container


