Build a Docker image file with sbt-pack
=======================================

#### Dockerfile
```dockerfile
FROM adoptopenjdk/openjdk8:jre8u282-b08-alpine

COPY target/pack /srv/myapp

USER somebody
WORKDIR /srv/myapp

ENTRYPOINT ["sh", "./bin/myapp"]
```

#### Build a docker image for a project
```shell
sbt pack
docker build -t your_org/myapp:latest .
```

#### Run the application with Docker
```shell
docker run -it --rm your_org/myapp:latest <args>
```
---
References:
1. [sbt-pack plugin](https://github.com/xerial/sbt-pack)
1. [Docker Images for OpenJDK Version 8 binaries built by AdoptOpenJDK](https://hub.docker.com/r/adoptopenjdk/openjdk8)
1. [Dockerizing Your Scala App](https://dzone.com/articles/dockerizing-your-scala-app)
