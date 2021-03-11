Docker
======

Build new image
---------------
```shell
docker build -t ${repo_name} . --no-cache
```

Save image to file
------------------
```shell
docker save -o ${filename}_image.tar ${repo_name}
```

Load image from file
--------------------
```shell
docker load -i ${filename}_image.tar
```

Run docker container
--------------------
```shell
docker run [-d] -p ${port}:${port} --name ${custom_name} ${repo_name}
```

View running containers
-----------------------
```shell
docker ps
```

Stop docker container
---------------------
```shell
docker stop ${container_id,custom_name}
```

View docker images
------------------
```shell
docker images
```

Remove docker image
-------------------
```shell
docker image rm ${image_id}
```

Access docker container
-----------------------
```shell
docker exec -it ${container_id} bash
```

