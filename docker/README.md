# Docker
> https://philipzheng.gitbook.io/docker_practice/


```
list containers
$ sudo docker container ls

enter container
$ sudo docker exec -it containerId bash


```


## docker-compose
### Running a new instance
```
$ sudo docker-compose -f docker.ymal -p projectName up -d
```

### Stop environment
$ sudo docker-compose -f docker.ymal -p projectName stop

### Restart stopped containers
$ sudo docker-compose -f docker.ymal -p projectName start

### Remove containers
$ sudo docker-compose -f docker.ymal -p projectName down -v

### Remove containers and all associated images
$ sudo docker-compose -f docker.ymal -p projectName --rmi all -v

