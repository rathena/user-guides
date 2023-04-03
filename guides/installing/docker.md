This guide covers how to quickly get rAthena running on any OS by using Docker. In depth docker topics will not be covered by this guide.

Code that you should run in your console/SSH application is `written like this`.

## What is Docker and why use it over a native installation?
One of the main benefits of Docker is the ability to replicate your environment, no matter the host OS, as you only need the Docker daemon/engine running and you're good to go.

## Pre-Requisites

### In General
* A basic understanding of Linux based Operating Systems.
* Familiarity with StackOverflow in case anything goes wrong

### Installing Requirements
First, you need to get Docker engine up and running. You can get this done by following the official [Docker guides](https://docs.docker.com/get-docker/). Once you get to the part where you install `docker-compose` you're good to go.

A few basic commands to remember:
* `docker-compose up -d` - This will start all the services defined in `docker-compose.yml` and detach the terminal. You can run without the `-d` to keep the logs attached.
* `docker-compose down` - If you have previously dettached, you can run this command next to the `docker-compose.yml` file to shut every service down gracefully.
* `docker logs <container name>` - Will print the last lines of logs of a given container
* `docker ps` - Will list all the containers you have _running_

### Understanding the docker-compose.yml
In this file you'll find how the magic really happens. Jokes aside, there's no magic, it's kinda easy once you wrap your head around it.

Inside the `services` block, you'll find every `service` a.k.a `container` we'll start once we run our `up` command.

1. Database
```yml
    db: # service name (this is the name docker uses to communicate to this container internally
        image: "mariadb:bionic" # container image (what it will be running)
        container_name: "rathena_db" # the name you'll be using to get logs or bash into
        ports: # this block will have the ports the container uses to make possible for you to connect to it from the host
            - "3306:3306" # allow DB connections from host
        volumes:
            - "rathenadb:/var/lib/mysql" # save database to local disk
            - "../../sql-files/:/docker-entrypoint-initdb.d" # initialize db with ./sql-files
        environment: # environment variables. self-explanatory
            MYSQL_ROOT_PASSWORD: ragnarok
            MYSQL_DATABASE: ragnarok
            MYSQL_USER: ragnarok
            MYSQL_PASSWORD: ragnarok
```

2. Builder  
This is a special container we've created so you're able to build the source without much hassle. That's because the other services (map/char/login) will crash and exit as soon as you start them, or if the server was already compiled they will start the server and then you won't be able to finish compiling.
```yml
    builder:
        image: "rathena:local"
        container_name: "rathena-builder"
        command: "/rathena/tools/docker/builder.sh" # this line will run the file linked once the container has started
        volumes:
            - "../..:/rathena" # mount git repo directory inside container
            - "./asset/inter_conf.txt:/rathena/conf/import/inter_conf.txt" # load db connection
            - "./asset/char_conf.txt:/rathena/conf/import/char_conf.txt"   # localdev login-char relation
            - "./asset/map_conf.txt:/rathena/conf/import/map_conf.txt"     # localdev char-map relation
        init: true # helps with signal forwarding and process reaping
        tty: true
        stdin_open: true
        build: # as we don't have an image available on the Docker hub for building and running rAthena, we need to build it ourselves
            context: .
            dockerfile: Dockerfile
        environment:
            BUILDER_CONFIGURE: "--enable-packetver=20211103" # here you can pass whatever you would pass to the `./configure` command
```

3. Login/Char/Map servers  
This part is where we define each of our executables/servers to run independently. The differences between the servers will be the `command` property which will contain the specific server that container will launch and the `depends_on` which specifies which other container should be up before initializing.
```yml
login:
        image: "rathena:local"
        container_name: "rathena-login"
        command: sh -c "/bin/wait-for db:3306 -- /rathena/login-server"
        ports:
            - "6900:6900" # login server
        volumes:
            - "../..:/rathena" # mount git repo directory inside container
            - "./asset/inter_conf.txt:/rathena/conf/import/inter_conf.txt" # load db connection
            - "./asset/char_conf.txt:/rathena/conf/import/char_conf.txt"   #localdev login-char relation
            - "./asset/map_conf.txt:/rathena/conf/import/map_conf.txt"     #localdev char-map relation
        init: true # helps with signal forwarding and process reaping
        tty: true
        stdin_open: true
        build:
            context: .
            dockerfile: Dockerfile
        depends_on:
            - db
```

### Setting up the server
1. After cloning the rAthena repo, you should open the project folder in the terminal. In my case I've cloned the project to `Documents/Personal/rathena`, so I've cd'ed to that folder.

<img width="575" alt="console" src="https://user-images.githubusercontent.com/13068064/229590462-9e7a85eb-6e98-4dfb-99ca-4d647ee0b819.png">

2. Then we can cd into `tools/docker` and then we can run the best command in the entire world `docker-compose up`. The very first time we do that command, it will pull the images from Docker hub and then build the server with the parameters specified in the `builder` service.
<img width="1506" alt="docker-compose up" src="https://user-images.githubusercontent.com/13068064/229595301-777c7e92-08f7-4a02-9c60-ca1ad440001a.png">

3. If we observe the logs, we'll be able to see that the `rathena-builder` container is yielding a bunch of logs. If you ever compiled with `make` you'll find those familiar.
<img width="545" alt="builder logs" src="https://user-images.githubusercontent.com/13068064/229595637-946c2541-d04c-4f65-87b1-2e48ca2659e5.png">
 
 4. After a while we can see that the compilation has finished once we see `rathena-builder exited with code 0`
<img width="616" alt="build finished" src="https://user-images.githubusercontent.com/13068064/229597246-9b00646b-e13d-4c4f-8212-8222023ab605.png">

5. Now all we need to do is `ctrl+c` to stop everything and then `docker-compose up`
<img width="1356" alt="start" src="https://user-images.githubusercontent.com/13068064/229597566-a8d38ab9-f2a6-4848-a95c-1fb5af1d39af.png">

And that's all about it. You've installed one thing on your host computer (a bit more if you count the depdencies to get docker runner) and now you have rAthena running. Once you stop the containers it will be like you never had a rAthena running on your machine.

### Recompiling
If you want to recompile so your changes are applied, all you gotta do is
1. First stop everything by hitting `ctrl+c` if you haven't dettached with `docker-compose up -d`
2. Run `docker-compose run builder bash`

This will start the builder container and give you access to its terminal, and from there you can run `make` commands to build like within any other VPS. Eg:

```bash
./configure --enable-packetver=20220404 --enable-pre-re --whatever-other-parameter
make server
```

### Additional info
You can find some more info on the `tools/docker` [README](https://github.com/rathena/rathena/blob/master/tools/docker/README.md)
