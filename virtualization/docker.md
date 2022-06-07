Docker
======

Commands
--------

#### Build new image

```shell
docker build -t ${repo_name} . --no-cache
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
```

#### View running containers

```shell
docker ps
```

#### Stop docker container

```shell
docker stop ${container_id,custom_name}
```

#### Restart a stopped container

```shell
docker restart ${container_id}
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
