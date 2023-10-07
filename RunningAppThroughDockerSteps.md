#This is after building the jar file
1. Update your Ubuntu system by running the following command:
```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo su
```
2. Install Docker 
```
sudo apt-get install docker.io -y
```
```
sudo systemctl enable docker
```
```
sudo systemctl start docker
```
```
sudo systemctl status docker
```
3. Navigate to the project directory
```
cd /home/ubadmin/spring-boot-mysql-example
```
4. Create docker file and Write the below content
```
vi Dockerfile
```
```
FROM openjdk:8
ADD target/spring-boot-mysql-0.0.1-SNAPSHOT.jar sbdapp.jar
ENV DBIP=${DBIP} DBPORT=${DBPORT} DBUSR=${DBUSR} DBPWD=${DBPWD}
ENTRYPOINT ["java", "-jar", "/sbdapp.jar"]
```
5. Build a docker image with docker file and verify
```
docker build -t spdimg .
```
```
docker images
```
6. Create and run a container for docker image
a. Run a container in differrent network (create docker network before assigning) :
```
docker run -itd --restart unless-stopped -p 8888:8080  --name sbd -e DBIP=172.17.0.1 -e DBPORT=3307 -e DBUSR=root -e DBPWD=password123 spdimg
```
b. Run a container in differrent network :
```
docker run -itd --restart unless-stopped -p 8180:8080 --network bridge2 --name sbdc springbootdocker -e DBIP=172.18.0.1 -e DBPORT=3306 -e DBUSR=root -e DBPWD=password123
```

```
docker ps
```
7. Browse the link [use your ip]
```
http://192.168.247.132:8080
```
8. Use below commands for starting or stopping the container
```
docker stop sbdc
```
```
docker start sbdc
```
9. Delete the Containers [names or ids given with space delimiter]
```
docker rm -rf <container names/ids>
```
10. Delete the images [names or ids given with space delimiter]
```
docker rmi imagenames/ids
```


