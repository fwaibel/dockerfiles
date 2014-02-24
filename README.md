dockerfiles
===========

## MongoDB

```text
$ cd TO_dockerfiles_GIT_REPOSITORY_ROOT
$ docker build -rm=true -t eclipsesource/mongodb mongodb 
```

Start the MongoDB container:

```	
docker run -p 27017:27017 -name mongodb -t eclipsesource/mongodb
```

## Virgo with Spring 3.2.5

```text
$ cd TO_dockerfiles_GIT_REPOSITORY_ROOT
$ docker build -rm=true -t eclipsesource/virgo-spring-325 virgo-spring-325 
```

Start the Virgo container with link to MongoDB, bind mount to /home/fwaibel/exchange/pickup and mapped network port 28080:

```
docker run -v /home/fwaibel/exchange/pickup:/home/virgo/pickup -p 28080:8080 -link mongodb:db -name virgo-spring-325 -t eclipsesource/virgo-spring-325
```
