# Docker Commands

```bash showLineNumbers

docker pc
too see command of docker

docker images
to see images present in local repocitory

donor docker pull {image name}
download image from docker hub (internet)

docker container ls
display list of running container in docker

docker container run -d alpine sh

docker container ls -a
it display list of all container that runned on docker

docker container run -it alpine sh
run alpine container and enter in their shell
-it means interactive terminal
sh means shell

docker image pull alpine:latest
download latest image of alpine

docker conatainer exec -it vigilant_borg bash Or docker conatainer exec -it {container Name} bash
enter in shell of running container

docker container stop vigilant_borg
stop container that run in background

docker container rm vigilant_borg
remove container that run in background

docker image build -t myapp:latest .
buid an image from dockerfile
-t means tag
{.} means docker file in current directory

docker container run -d --name web1 -p 8080:8080 test:latest
--name means name of container
-p port settings
first port number is for host
second prot number is for container
test means image name
latest means tag for image

docker login
to login in docker hub

docker tag testapp:latest usamajamil/testapp:latest
Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

docker push usamajamil/testapp:latest
push image to docker hub

docker image build -t sqlserver:v1 .
sqlserver means image name
v1 means tag of image

docker run --name test-html -d -p 9000:80 testhtml:latest
9000 means host port
80 means container port
-d means deamon mode

docker container ls
list of running container

docker container run -it -v /user/document/demov:/test alpine
-v means sync host volume to local to container
/user/document/demov host volume
/test containrer Volume

docker image rm $(docker image ls -q) -f
remove all images in local repository

docker image ls -q
return all list of image IDs

$ docker container rm $(docker container ls -aq) -f
-f means force so running process in container also be destroyed

docker engine
? deamon
? containerd
? runc

runc

As previously mentioned, runc is the reference implementation of the OCI container-runtime-spec. Docker, Inc. was heavily involved in defining the spec and developing runc.

containerd
In order to use runc, the Docker engine needed something to act as a bridge between the daemon and runc.

We mentioned earlier that containerd uses runc to create new containers.

```

Commands:

**docker compose**

installation:

**Install Docker Engine**

```bash showLineNumbers
sudo apt-get install docker-compose-plugin
```

https://docs.docker.com/engine/install/ubuntu/

to show list of docker image running

```bash showLineNumbers
docker ps
```

command to up service in docker compose

```bash showLineNumbers
docker compose up <service-name> -d (detach mode aka background mode)
docker compose up hefazatapi-db -d
```

### For mac

**Dont forgot to start docker service before run docker command:**

make sure you start docker program in your process by just search from installed app of docker and open it

and in order to open automatically when you login to computer check this below line in docker preference settings.

`Start Docker Desktop when you log in`

### top-5-tips-for-docker-image-optimization

https://medium.com/@fatimamaryamrauf/top-5-tips-for-docker-image-optimization-3ba4e25557fb

**how to stop docker container**

Commands

```bash showLineNumbers
$ docker ps (show running conatainer only)
$ docker ps -a (show all containers running + stopped)
$ docker stop <container-id> (to stop running container)
$ docker rm <container-id> (to remove container from local storages)

or
$ docker stop <container-name>
```

https://www.baeldung.com/ops/docker-stop-vs-kill

**Command to see docker container logs**

```bash showLineNumbers
$ docker logs --follow hefazatapi (to see logs of docker container)
```

**command to follow logs**

```
docker logs <server-name> -f
```

https://docs.docker.com/engine/reference/commandline/logs/

**Issue with Lodash Throttle or Debounce within the loop**

In reply to the comment:
In that case, throttle maybe is not the right choice. You might want to use asynchronous function by using Promise.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

```jsx showLineNumbers
function asyncDoSomething(i) {
  return new Promise((resolve, reject) => {
    console.log("Doing something: " + i);
    setTimeout(() => {
      resolve(i);
    }, 15000);
  });
}

async function doSomethingLoop() {
  for (var i = 0; i < 50; i++) {
    await asyncDoSomething(i);
  }
}

doSomethingLoop();
```

https://stackoverflow.com/questions/55789104/issue-with-lodash-throttle-or-debounce-within-the-loop
