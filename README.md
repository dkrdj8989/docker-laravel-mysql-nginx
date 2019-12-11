# docker-laravel-mysql-nginx
This is for development environment use 

<br>
To build the environment make sure you are in your projects root folder and run docker-compose build and let it run

#install 
first of all 
create "www" folder in the root folder
```
docker-compose build
```
```
docker-compose up -d
```

#check docker images
```
docker images
```

#check docker container 
 ```
docker ps -a 
```

#remove docker image
```
single : docker rmi [image name] 
all : docker image prune -a 
```

#remove docker container
```
single : docker rm [container name]
all : docker rm -f `docker ps -a -q`
```