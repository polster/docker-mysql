# MySQL Docker Image

## Environment

* CentOS 7
* MySQL community server 5.6.26

## User Guide

### Prepare

* Build the image:
```
docker build --rm --tag <user>/<image name> .
```
* Show available images:
```
docker images
```

### Run Container

#### Quick and dirty

* Simply start a new container for development or testing (not recommended for production):
```
docker run --name=<container name> -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<password> <user>/<image name>
```

#### Recommended

* Create a separate data container which will only be run once at the time it is being created/started; allowing us to change the separate container which contains the DB process without losing data:
```
docker run --name=<container name>-data -v /var/lib/mysql <user>/<image name> true
```
* Create and start the effective container where the DB process is running on:
```
docker run --name=<container name> -d -p 3306:3306 --volumes-from=<image name>-data -e MYSQL_ROOT_PASSWORD=<password> <user>/<image name>
```