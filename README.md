# BAZO-Docker
This is a lightweight development environment for BAZO.

### Why do we need a development environment?
The idea is that every contributor working on BAZO uses the same software stack. (Linux, GO version, Postgres version). Plus, you don't go through the trouble of installing all these dependencies on your local machine.

## Get Started
#### Prerequisite
[Docker](https://www.docker.com/) must be installed (version 2.3.0.4 or higher) on your machine.

#### Installation Guide
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
Open the hosts file in your editor of choice. The hosts file is located 
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
Thats it! The project will be built and a miner, client and block-explorer will be launched

Open a browser and checkout http://bazo.local:8080