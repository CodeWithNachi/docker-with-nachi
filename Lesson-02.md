# Lesson 02

## Intention
 * Understand the similarity between Docker Containers and Virtual machines
 * Run commands in containers
 * Copy contents to and from containers

# Experiment 01
 * 
 * /usr/share/nginx/html 
 * docker exec -w /usr/share/nginx/html mynginx ls
 * docker exec -w /usr/share/nginx/html mynginx cat index.html

# Experiment 02
 * docker exec -w /usr/share/nginx/html mynginx sh -c 'echo "hello" > ./mypage.html'
 * docker exec -w /usr/share/nginx/html mynginx ls
 * localhost:8090/mypage.html

# Experiment 03
 * docker exec -w /usr/share/nginx/html mynginx -it /bin/bash
 * cat /etc/os-release
 * apt update
 * 
 
 
