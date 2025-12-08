Docker
======

Commands
--------

#### Build new image

```shell
docker build -t ${repo_name} . --no-cache

# in a multi-container project use docker compose instead
docker compose [-f ${custom_name}.yml] up

# or force image rebuild
docker compose [-f ${custom_name}.yml] build --no-cache
```

#### Save image to file

```shell
docker save -o ${filename}_image.tar ${repo_name}
```

#### Load image from file

```shell
docker load -i ${filename}_image.tar
```

#### View docker images

```shell
docker images
```

#### Remove docker image

```shell
docker image rm ${image_id}
```

#### Run docker container

```shell
docker run [-d] -p ${port}:${port} --name ${custom_name} ${repo_name}

# in a multi-container project use docker compose instead
docker compose [-f ${custom_name}.yml] up -d
```

#### View running containers

```shell
docker ps
```

#### Stop docker container

```shell
docker stop ${container_id,custom_name}

# in a multi-container project use docker compose instead
docker compose [-f {custom_name}.yml] stop

# or stop and tear down all containers for update or maintenance
docker compose [-f {custom_name}.yml] down
```

#### Start stopped docker container
```shell
docker start ${container_id,custom_name}

#  in a multi-container project use docker compose instead
docker compose [-f {custom_name}.yml] start
```

#### Restart a stopped container

```shell
docker restart ${container_id}

# in a multi-container project use docker compose instead
docker compose [-f {custom_name}.yml] restart
```

#### Remove a container

```shell
docker rm ${container_id}
```

#### Remove all containers at once

```shell
docker rm $(docker ps -aq)
```

#### Remove build cache

```shell
docker builder prune
```

#### Access docker container

```shell
docker exec -it ${container_id} bash

# in a multi-container project use docker compose instead
docker compose [-f {custom_name}.yml] exec ${service} ${command} ${arguments}
```

#### Pass input from a file to a docker container

Linux:
```shell
docker exec <arguments> < my/input/file
```

Windows (Powershell):
```powershell
Get-Content -Path .\my\input\file | docker exec <arguments>
```
