---
sort: 1
---

# Volume --> Persitent Data

## What we will see here
* Creation of volume which is outside the container 
* Volume outlive the containers and has to be deleted manually

# Experiment 1
 * Lets run an mysql container with the below command
```bash
docker  run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
```
* Now if you do a docker inspect you should be able to  the below output under mounts which will show a unique location under host to store the date


