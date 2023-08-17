## INSTALL DOCKER

A very detailed instructions to install Docker are provide in the below link

https://docs.docker.com/get-docker/

For Demo, 

You can create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```
sudo apt update
sudo apt install docker.io -y
```


### Start Docker and Grant Access

A very common mistake that many beginners do is, After they install docker using the sudo access, they miss the step to Start the Docker daemon and grant acess to the user they want to use to interact with docker and run docker commands.

Always ensure the docker daemon is up and running.

A easy way to verify your Docker installation is by running the below command

```
docker run hello-world
```

If the output says:

```
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This can mean two things, 
1. Docker deamon is not running.
2. Your user does not have access to run docker commands.


### Start Docker daemon

You use the below command to verify if the docker daemon is actually started and Active

```
sudo systemctl status docker
```

If you notice that the docker daemon is not running, you can start the daemon using the below command

```
sudo systemctl start docker
```


### Grant Access to your user to run docker commands

To grant access to your user to run the docker command, you should add the user to the Docker Linux group. Docker group is create by default when docker is installed.

```
sudo usermod -aG docker ubuntu
```

In the above command `ubuntu` is the name of the user, you can change the username appropriately.

**NOTE:** : You need to logout and login back for the changes to be reflected.


### Docker is Installed, up and running 🥳🥳

Use the same command again, to verify that docker is up and running.

```
docker run hello-world
```

Output should look like:

```
....
....
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
...
```


## Great Job, Now start with the examples folder to write your first Dockerfile and move to the next examples. Happy Learning :)

### Clone this repository and move to example folder

```
git clone https://github.com/iam-veeramalla/Docker-Zero-to-Hero
cd  examples
```

### Login to Docker [Create an account with https://hub.docker.com/]

```
docker login
```

```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: abhishekf5
Password:
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### Build your first Docker Image

You need to change the username accoringly in the below command

```
docker build -t abhishekf5/my-first-docker-image:latest .
```

Output of the above command

```
    Sending build context to Docker daemon  992.8kB
    Step 1/6 : FROM ubuntu:latest
    latest: Pulling from library/ubuntu
    677076032cca: Pull complete
    Digest: sha256:9a0bdde4188b896a372804be2384015e90e3f84906b750c1a53539b585fbbe7f
    Status: Downloaded newer image for ubuntu:latest
     ---> 58db3edaf2be
    Step 2/6 : WORKDIR /app
     ---> Running in 630f5e4db7d3
    Removing intermediate container 630f5e4db7d3
     ---> 6b1d9f654263
    Step 3/6 : COPY . /app
     ---> 984edffabc23
    Step 4/6 : RUN apt-get update && apt-get install -y python3 python3-pip
     ---> Running in a558acdc9b03
    Step 5/6 : ENV NAME World
     ---> Running in 733207001f2e
    Removing intermediate container 733207001f2e
     ---> 94128cf6be21
    Step 6/6 : CMD ["python3", "app.py"]
     ---> Running in 5d60ad3a59ff
    Removing intermediate container 5d60ad3a59ff
     ---> 960d37536dcd
    Successfully built 960d37536dcd
    Successfully tagged abhishekf5/my-first-docker-image:latest
```

### Verify Docker Image is created

```
docker images
```

Output 

```
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
abhishekf5/my-first-docker-image   latest    960d37536dcd   26 seconds ago   467MB
ubuntu                             latest    58db3edaf2be   13 days ago      77.8MB
hello-world                        latest    feb5d9fea6a5   16 months ago    13.3kB
```

### Run your First Docker Container

```
docker run -it abhishekf5/my-first-docker-image
```

Output

```
Hello World
```

### Push the Image to DockerHub and share it with the world

```
docker push abhishekf5/my-first-docker-image
```

Output

```
Using default tag: latest
The push refers to repository [docker.io/abhishekf5/my-first-docker-image]
896818320e80: Pushed
b8088c305a52: Pushed
69dd4ccec1a0: Pushed
c5ff2d88f679: Mounted from library/ubuntu
latest: digest: sha256:6e49841ad9e720a7baedcd41f9b666fcd7b583151d0763fe78101bb8221b1d88 size: 1157
```

### You must be feeling like a champ already 
