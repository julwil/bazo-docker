# BAZO-DOCKER
<!-- language: lang-none -->
      ____               ______   ____             _____     ____     _____   _  __  ______   _____  
     |  _ \      /\     |___  /  / __ \           |  __ \   / __ \   / ____| | |/ / |  ____| |  __ \ 
     | |_) |    /  \       / /  | |  | |  ______  | |  | | | |  | | | |      | ' /  | |__    | |__) |
     |  _ <    / /\ \     / /   | |  | | |______| | |  | | | |  | | | |      |  <   |  __|   |  _  / 
     | |_) |  / ____ \   / /__  | |__| |          | |__| | | |__| | | |____  | . \  | |____  | | \ \ 
     |____/  /_/    \_\ /_____|  \____/           |_____/   \____/   \_____| |_|\_\ |______| |_|  \_\ 
                                                                                                 
This is a lightweight development environment for BAZO.

### Why do we need a development environment?
- Everyone uses the exact same stack. (Linux version, GO version, Postgres version).
- No need to clutter your machine with dependencies.
- No need to go through the trouble of installing and configuring each project.
- Run your code on isolated containers.
- Use your favorite IDE to code. The code will be shared with the containers.

## Getting Started
#### Prerequisite
[Docker](https://www.docker.com/) must be installed (version 2.3.0.4 or higher) on your machine. [More...](#installing-docker-on-windows)

#### Quick Start
on your machine, create a new folder and cd into it 
```
mkdir CSG-BAZO/
cd CSG-BAZO/
```

clone the `bazo-miner` repository
```
git clone https://github.com/julwil/bazo-miner
```

clone the `bazo-miner` repository
```
git clone https://github.com/julwil/bazo-miner
```

clone the `bazo-client` repository
```
git clone https://github.com/julwil/bazo-client
```

clone the `bazo-block-explorer` repository
```
git clone https://github.com/julwil/bazo-block-explorer
```

##### IMPORTANT
If your repos are forked form another repository, you need to fix the imports.

In each repository, you will find a bash script `fix-imports.sh`. Run each of them, it will prompt for your GitHub username.
```shell script
cd bazo-miner
./scripts/fix-imports.sh
```
```shell script
cd bazo-client
./scripts/fix-imports.sh
```
```shell script
cd bazo-block-explorer
./scripts/fix-imports.sh
```
next, we need to set entries for the hosts file of our machine

##### Windows: 
- open the Windows Notepad application with **admin rights**. (Run as Administrator)
- Open `C:\Windows\System32\drivers\etc\hosts` file and add the following entries at the end of the file.
These entries will route a request to http://bazo.local and http://api.bazo.local to the IP 127.0.0.1 (your localhost).
```
#CSG-BAZO Project
127.0.0.1 bazo.local
127.0.0.1 api.bazo.local
```
- Save the file.

##### Mac/Linux: 
- open a new Terminal session.
- When prompted, enter your password.
Open the hosts file in your editor of choice. The hosts file is located in `etc/hosts`
```shell script
nano /etc/hosts
```
Add the following entries at the end of the file. These entries will route a request to http://bazo.local and http://api.bazo.local to the IP 127.0.0.1 (your localhost).
```
#CSG-BAZO Project
127.0.0.1 bazo.local
127.0.0.1 api.bazo.local
```
- Save the file by pressing `cmd + s` or `ctrl + s`

Next, cd into the `bazo-docker` directory and start docker-compose
```shell script
cd bazo-docker
docker-compose up
```
This will build all your code and launches a fresh cluster of the application.
The applications consists of a started miner, a client which serves the REST API, as well as the block-explorer.

That's it! Open a browser and checkout http://bazo.local:8080

## Installing Docker on Windows
Docker is now available for all Windows versions (Home, Pro,...) thanks to the integration of Windows Subsystem for Linux 2 (WSL2).
Check out the [official documentation](https://docs.docker.com/docker-for-windows/install/) on Docker for Windows

#### Installation guide
- Enable virtualization in the BIOS of your machine [More...](https://www.bleepingcomputer.com/tutorials/how-to-enable-cpu-virtualization-in-your-computer-bios/#:~:text=CPU%20Virtualization%20is%20a%20hardware,it%20was%20multiple%20individual%20CPUs.&text=Unfortunately%2C%20in%20many%20cases%20CPU,to%20take%20advantage%20of%20it.)
- Follow **exactly** [this guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to enable WSL, Update to WSL2, and set WSL2 as your default version
- Finally, install Docker from [this resource](https://docs.docker.com/docker-for-windows/install-windows-home/).

## Installing Docker on Mac
Check out the [official documentation](https://docs.docker.com/docker-for-mac/install/) on Docker for Mac.

## Installing Docker on Linux
Check out the [official documentation](https://docs.docker.com/engine/install/ubuntu/) on Docker for Ubuntu.


## Know-How & Gotchas
#### Source code
Source code is shared between the host and the docker containers. That's why it is important to stick to the folder structure explained in the [Quick Start](#quick-start). As soon as the application started, you will see log files in the `bazo-miner/` folder. You can use an IDE of your choice to code.

#### docker-compose up doesn't work
If you have trouble with `docker-compose up`, make sure you are in the `bazo-docker/` directory. Alternatively, you can provide the docker-compose file with the `-f <path/to/file>` flag.

#### Changing docker configuration
If you change the Docker configuration, make sure you `docker-compose down && docker-compose up -- build` to see your changes come into effect. If that doesn't help, try `docker system prune -a` which wipes everything clean. Also, sometimes it helps restarting Docker Desktop.
Always document changes in the docker-compose.yml and the Dockerfile!

#### Dockerfile and docker-compose.yml
In the root of this directorly, you find the `docker-compose.yml` file. It ties everything together.
In the `docker-compose.yml` file you define all the services that make up your application. Here you can define port forwarding, networking, dependencies between services.

In the directory of each project `bazo-miner`, `bazo-client`, and `bazo-block-explorer`  you find a `Dockerfile`. It defines the docker-image on which the container is based. Here you install, build and define a RUN or CMD command for your container.