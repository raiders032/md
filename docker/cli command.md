## 

## docker build

> Build an image from a Dockerfile

```shell
docker build [OPTIONS] PATH | URL | -
```



| Options     | Description                                             |
| ----------- | ------------------------------------------------------- |
| --build-arg | Set build-time variables                                |
| --tag , -t  | Name and optionally a tag in the ‘name:tag’ format      |
| --rm        | Remove intermediate containers after a successful build |
| --file , -f | Name of the Dockerfile (Default is ‘PATH/Dockerfile’)   |
|             |                                                         |
|             |                                                         |
|             |                                                         |



예시

```shell
docker build -t neptunes032/react-test-app -f ./frontend/Dockerfile.dev ./frontend

docker build -t neptunes032/docker-frontend ./frontend

docker build .
```



___



## docker commit

> Create a new image from a container’s changes

```shell
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

___



## docker container ls

> List containers

```
docker container ls [OPTIONS]
```

___



## docker container prune

> Remove all stopped containers

```
docker container prune [OPTIONS]
```

| Options        | Descripton                            |
| :------------- | ------------------------------------- |
| --filter       | Provide filter values (e.g. ‘until=') |
| `--force , -f` | Do not prompt for confirmation        |



___



## docker container rm

> Remove one or more containers

```
docker container rm [OPTIONS] CONTAINER [CONTAINER...]
```

___



## docker exec

> Run a command in a running container

```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

| Options             | Descripton                                            |
| :------------------ | ----------------------------------------------------- |
| --detach , -d       | Detached mode: run command in  the background         |
| --detach-keys       | Override the key sequence for  detaching a container  |
| --env  , -e         | Set environment variables                             |
| --interactive  , -i | Keep STDIN open even if not attached                  |
| --privileged        | Give extended privileges to the  command              |
| --tty ,  -t         | Allocate a pseudo-TTY                                 |
| --user  , -u        | Username or UID (format:  <name\|uid>[:<group\|gid>]) |
| --workdir  , -w     | Working directory inside the container                |



예시

```
docker exec -it jenkins /bin/bash
```



___



## docker images

> List images

```
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

___



## docker image ls

> List images

```
docker image ls [OPTIONS] [REPOSITORY[:TAG]]
```

___



## docker image prune

> Remove unused images

```
docker image prune [OPTIONS]
```

| Options      | Description                                      |
| ------------ | ------------------------------------------------ |
| --all , -a   | Remove all unused images, not just dangling ones |
| --filter     | Provide filter values (e.g. ‘until=')            |
| --force , -f | Do not prompt for confirmation                   |

___



## docker image rm

> Remove one or more images

```
docker image rm [OPTIONS] IMAGE [IMAGE...]
```



예시

```shell
# 모든 이미지 삭제
docker image rm $(docker images -q) 

```

___



## docker inspect

> Return low-level information on Docker objects

```
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

___



## docker logs

> Fetch the logs of a container

```
docker logs [OPTIONS] CONTAINER
```

| Options           | Description                                      |
| ----------------- | ------------------------------------------------ |
| --follow , -f     | Follow log output                                |
| --tail            | Number of lines to show from the end of the logs |
| --timestamps , -t | Show timestamps                                  |



___



## docker network ls

> List networks

```shell
docker network ls [OPTIONS]
```

___



## docker ps

> List containers

```
docker ps [OPTIONS]
```

| Options      | Description                                      |
| ------------ | ------------------------------------------------ |
| --all , -a   | Show all containers (default shows just running) |
| --quiet , -q | Only display numeric IDs                         |
|              |                                                  |



예시

```shell
// 모든 컨테이너 삭제
docker rm `docker ps -a -q`
```



___



## docker pull

>  Pull an image or a repository from a registry

```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

___



## docker push

> Push an image or a repository to a registry

```
docker push [OPTIONS] NAME[:TAG]
```

___



## docker run

> Run a command in a new container

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```



| Options            | Description                                        |
| ------------------ | -------------------------------------------------- |
| --attach , -a      | Attach to STDIN, STDOUT or STDERR                  |
| --detach , -d      | Run container in background and print container ID |
| --env , -e         | Set environment variables                          |
| --interactive , -i | Keep STDIN open even if not attached               |
| --publish , -p     | Publish a container’s port(s) to the host          |
| --rm               | Automatically remove the container when it exits   |
| --volume , -v      | Bind mount a volume                                |
| --tty , -t         | Allocate a pseudo-TTY                              |
|                    |                                                    |



예시

```shell
docker run -e CI=true neptunes032/react-test-app npm run test
docker run -p 3000:80 -d --name feedback-app --rm feedback-node
```



### Publish or expose port (-p, --expose)

> This binds port `8080` of the container to TCP port `80` on `127.0.0.1` of the host machine. You can also specify `udp` and `sctp` ports. The [Docker User Guide](https://docs.docker.com/network/links/) explains in detail how to manipulate ports in Docker.

```
docker run -p 127.0.0.1:80:8080/tcp ubuntu bash
```

___

## docker rm

> Remove one or more containers

```shell
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

| Options        | Description                                             |
| -------------- | ------------------------------------------------------- |
| --force , -f   | Force the removal of a running container (uses SIGKILL) |
| --link , -l    | Remove the specified link                               |
| --volumes , -v | Remove anonymous volumes associated with the container  |



예시

```
# 모든 도커 컨테이너 제거
docker rm $(docker ps -a -q)
```





___





## docker start

> Start one or more stopped containers

```
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

___



## docker stop

> Stop one or more running containers

```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

예시

```shell
# 구동중인 모든 컨테이너 중지
docker stop $(docker ps -a -q)

```



___

## docker tag

> Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

```shell
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

