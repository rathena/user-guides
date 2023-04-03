This guide covers how to install rAthena on Debian 10. For earlier versions of Debian you may need to alter the list of required packages. Older versions will not be covered in this guide.

Code that you should run in your console/SSH application is `written like this`.

This guide covers the installation via CLI and *does not* include instructions for installing a desktop environment for use with a VNC server.

## Pre-Requisites

### In General
* A basic understanding of Linux based Operating Systems.
* A basic understanding of the SSH tool Putty.
* A basic understanding of MySQL (or RDBMS in general).
* A basic understanding of when the root system user should be used, and when you should use a standard user shell.
* A basic understanding that "if at first you don't succeed, search the forums" will be your saving-grace in the event of errors.

### Debian 10
You should ensure that your system is up-to-date by first: `apt-get update`

### Installing Requirements
We need the following applications to compile rAthena on Debian 10:
```
apt-get install git make libmariadb-dev libmariadbclient-dev libmariadbclient-dev-compat gcc g++ zlib1g-dev libpcre3-dev
```
You can install the above applications, and any following applications as root, then we'll switch to a standard user later on in the guide.

If you don't feel comfortable editing files in Vim, you should install nano:
```
apt-get install -y nano
```

### MySQL
For the installation instructions of MySQL, please see the [relevant installation page](https://github.com/rathena/rathena/wiki/Install-MySQL#linux).


## The Code Repository

rAthena uses git for revision control, and hosts the git repository on Github.

### Cloning 
You can obtain the latest version of rAthena by typing the following command. This will place rAthena in a folder called rAthena in your home directory, but you are free to change it to whatever you like:

```
git clone https://github.com/rathena/rathena.git ~/rAthena
```


### Updating

To pull the latest updates for rAthena you can do the following:
```
git pull
```


## Compile The Code

There are several steps you will need to do now in order to run rAthena. You first need to run the "configure script" to ensure everything is working as it should, and to build necessary make-files.
```
./configure
```

The next command is not essential *every* time you compile, but it helps to ensure caches are removed when compiling.
```
make clean
```

And then finally, we're going to build the server's code.
```
make server
```

Potentially, you may need to `chmod` your server binaries to make them "executable".
```
chmod a+x login-server && chmod a+x char-server && chmod a+x map-server && chmod a+x web-server
```

## Recompile The Code

Recompiling is the same as compiling. You can throw the code into a one-liner, if you like.
```
./configure && make clean && make server
```


## Starting rAthena
The provided method of running rAthena will work perfectly fine, but this author's personal preference is shown below as an *alternative method*.

### Provided Method
Use the following commands
* To Start:

    `./athena-start start`

* To Stop:

    `./athena-start stop`

* To Restart:

    `./athena-start restart`


If you receive an error similar to the following:
```
-bash: ./athena-start: /bin/sh^M: bad interpreter
```

You can install dos2unix with `apt-get install dos2unix` and then run `dos2unix athena-start`.

You will now be able to use `./athena-start start` after `chmod a+x athena-start`.

### Alternative Method
Firstly, install `screen`:
```
apt-get install -y screen
```
You can then keep all your separate consoles running in the background, and call them forward individually whenever you like.

First, create the sessions:
```
screen -dmS login
screen -dmS char
screen -dmS map
screen -dmS web
```

Then you can connect to each one individually like so:
```
screen -r login
```
When you are inside the session, `cd` to your rAthena folder and start the login-server, e.g. `cd ~/rAthena && ./login-server`. This should now start the login-server. To detach from the session while keeping the login-server running, you will need to hold down the `Ctrl` key on your keyboard and then press the `A` and `D` keys at the same time. Then, do the same to the other servers. If you want to terminate any of your servers, you will need to resume the session (`-r`) and then `Ctrl` + `C`.

To make sure your sessions are still running, you can `screen -ls` which will output something similar to:
```
[athenauser@vps-ba60c6aa ~]$ screen -ls
There are screens on:
        32121.login      (Detached)
        4146.web         (Detached)
        4115.map         (Detached)
        4088.char        (Detached)
4 Sockets in /var/run/screen/S-athenauser.
```

### Connections
If you've just started your servers and get some errors, don't worry, it's because you haven't configured them yet.

We have a handy guide [here](https://github.com/rathena/rathena/wiki/connecting) that will talk you through what you need to change in order to get your servers up and running successfully.
