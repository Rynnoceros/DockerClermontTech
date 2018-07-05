# DockerClermontTech
Présentation Clermont Tech

# Docker

## Intro

https://training.play-with-docker.com

### Tools

    Kitematic: outil caché de docker (github docker)
    Outil de lancement container docker
    => Gère volume, réseau...

### Terminology
    Image pulled from Docker Store

### Commands

* docker image run [name]
* docker image pull [name]
* docker image ls
* docker container ls
* docker container ls -a
    * Prefetch system
* docker container ps (old syntax)
* docker container rm [id]
    * --force
* docker container run alpine ls -l
* docker container run alpine /bin/sh
    * Auto exited
* docker container run -it alpine /bin/sh
    * it option for Interactive Terminal
* docker container kill [id]
* docker container start [id]
* docker container exec [id] command
* docker system prune
    * remove all killed container and images
    * pseudo-tty
        * Pseudo terminal Unix tty
* docker container logs mydb
    * Logs system
* docker container top mydb
    * Process displayer UNIX

### Multilines
    docker container run \
    --detach \
    --name mydb \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    mysql:latest


 --detach will run the container in the background.

 --name will name it mydb.

 -e will use an environment variable to specify the root password (NOTE: This should never be done in production).

 ### History commands
    docker exec -it mydb \
    mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version

 * docker exec -it mydb sh
    * container removed

* cat Dockerfile
    * See content of file
    * nginx
        * Serveur web

### Dockerfile
    List of commands to build image


    FROM specifies the base image to use as the starting point for this new image you’re creating. For this example we’re starting from nginx:latest.
    COPY copies files from the Docker host into the image, at a known location. In this example, COPY is used to copy two files into the image: index.html. and a graphic that will be used on our webpage.
    EXPOSE documents which ports the application uses.
    CMD specifies what command to run when a container is started from the image. Notice that we can specify the command, as well as run-time arguments.

    => Sample: 
    FROM nginx:latest

    COPY index.html /usr/share/nginx/html
    COPY linux.png /usr/share/nginx/html

    EXPOSE 80 443

    CMD ["nginx", "-g", "daemon off;"]

docker run --rm -d -p 80:80 nginx
    bind le port 80 sur le 80

curl localhost:80

docker image build --tag linux_tweet_app:1.0 .
-- tag => Nom de l'image. Le . final est la location

docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 --mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \ linux_tweet_app:1.0

docker commit running_container > new_image:version

docker container diff [id]

docker image tag <IMAGE_ID> ourfiglet
docker container run ourfiglet figlet hello


apt-get update
apt-get install -y figlet
figlet "hello docker"

=> figlet display

### Liens pour faire joujou

* https://training.play-with-docker.com/ops-s1-hello/
* https://training.play-with-docker.com/beginner-linux/
* https://training.play-with-docker.com/ops-s1-images/
* https://training.play-with-docker.com/docker-volumes/
* https://docs.docker.com/kitematic/userguide/
