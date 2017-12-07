

# Introducing Containers

## Docker 
Layer
Layer1 -> Docker Engine
            * libcontainer  control cross platform
Layer1.1 -> LXC  alexcy  docker us LXC
Layer2 -> Operating System
            * Namespaces 
            * cgroups
            * Capabilities
Layer3 -> Physical or Virtual Server



# Installing Ubuntu Linux and CentOS Linux

## download ubuntu server
dowonload version LTS becouase is long term support.
## create virtual machine Ununtu Server
recommanded 
    * OS Type:Linux, Version:Red Hat (64 bit)
    * Memory size 1 MB (up to you)
    * Harddisk size 20 GB (up to you)
    * Hard drive file type is 'VDI (VirtualBox Disk Image)
    * Storage on physical hard drive 'Dynamically allocated'
    * Network
        - Adapter 1 : NET
        - Adapter 2 : Host-only Adapter
## Install Ubuntu Server 16.04.03
- US
- Asia
- Thailand
Configure the keyboard
- <No>
    - Thai

Partitioning disk
- Guided - use entire disk and set up LVM

    Write the changes to disks and configure LVM?
    - <Yes>
    add   80% 

    Software selection
    - standarrd system utilities
    - OpenSSH server

## download CentOS 7 1604
download CentOS  DVD ISO version
## create virtual machine CentOS
recommanded 
    * OS Type:Linux, Version:Ubuntu (64 bit)
    * Memory size 1 MB (up to you)
    * Harddisk size 20 GB (up to you)
    * Hard drive file type is 'VDI (VirtualBox Disk Image)
    * Storage on physical hard drive 'Dynamically allocated'
    * Network
        - Adapter 1 : NET
        - Adapter 2 : Host-only Adapter

## Install CentOS 7 1604
- select leanguage installation

PAGE: INSTALLATION SUMMARY
- SYSTEM -> INSTALLATION DESTINATION
    - valify check Local Storage 
    - Other Storage Options -> Partitioning : Choose 'Automatically configure partitioning'
- SOFTWARE SELECTION
    - Choosed 'GNOME Desktop'
- NETWORK & HOST NAME
    - Ethernet (enpOs3) switch [Turu On] Network adapter.
    - Ethernet (enpOs8) switch [Turu On] Network adapter.
click Installation.

PAGE: CONFIGURATION
USER SETTINGS
- ROOT PASSWORD
    * change your root password 'A@Tonhoam54'
- USER CREATION
    * fullname :  'Pichit Sripirom'
    * user: 'psripirom'
    * password: 'A@Tonhoam54'

- Reboot.
- Accept License
- Check Network  switch On all Adapters.
# ===================================================================

# Installing and Updating Docker ====================================


Ubuntu 16

Ubuntu 16
add enp0s8 below:
auto enp0s3
iface enp0s3 inet dhcp

auto enp0s8
iface enp0s8 inet static
address 192.168.99.50  (Enter desired ip here)
netmask 255.255.255.0
network 192.168.99.0
broadcast 192.168.99.255
gateway 192.168.99.1

$ docker -v
docker version 1.12.6 build 78d1802


$ uname -
show  linux os version


## setting network host only

Ubuntu 14
$ vi /etc/interfaces
add eth1 below:
auto eth1
iface eth1 inet static
address 192.168.99.50  (Enter desired ip here)
netmask 255.255.255.0
network 192.168.99.0
broadcast 192.168.99.255
gateway 192.168.99.1

key esc
key :
type wq  enter.


$ sudo sh -c "echo deb https://get.docker.io/ubuntu docker main \
> /etc/apt/sources.list.d/docker.list"
$ sudo apt-get update
$ sudo apt-get install lxc-docker

## Installing Docker on Ubuntu -----------------------------------
$ apt-get update
$ apt-get install -y docker.io

$ service docker status
docker start/running process 2620

$ docker -v
Docker version 1.6.2, build 7c8fca2

$ docker version
show all components.

$ docker info
show server infomation
show containers
storage driver: aufs     // if CentOS is devicemapper



## Updating Docker
$ docker -v
Docker version 1.6.2, build 7c8fca2

$ wget -qO- https://get.docker.com/gpg | apt-key add -
OK

$ echo deb http://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list

$ apt-get update

now we're calling the Docker package lxc-docker
$ apt-get install lxc-docker

$ docker version
show version 1.9.1

## Granting Docker Control to Non-root Users
Binds to /var/run/docker.sock

$ ls -l /run
You can see the Docker socket there
-rw-r--r-- 1 root       root         60 Aug 13:01:27 docker

Docker instead of needing to be root to run Docker

exit root
$ exit

Dead sample. "run with out 'root'"
$ docker run -it ubuntu /bin/bash

$ cat /etc/group
....
docker:x:112

// add permission user pichit to docker gorup
$ sudo gpasswd -a pichit docker

$ cat /etc/group
......
docker:x:112:pichit

// logoff to reset permission
$ logout
login agian 

$ docker run -it ubuntu /bin/bash
you can install container. then auto login to root


## Installing Docker on CentOS
login: root
install docker
$ yum install -y docker

Let's see running
$ systemctl status docker.service
response status Dead

Let's start
$ systemctl start docker.service

checking version
$ docker -v 
Docker version 1.12.6, build 88a4867/1.12.6

$ docker version
show all components.

$ docker info
show server infomation
show containers
storage driver: devicemapper     // if CentOS is aufs


## Configuring Docker to Communicate Over the network


check version on Ubuntu is "Docker version 1.9.1"
Client API version 1.21

check version on CentOS is "Docker version 1.12.6"
Client API version 1.24

On Ubuntu
    $ sudo su 
    check network port Unbuntu
    $ netstat -tlp
    show  ssh listening

    setting docker network
    $ service docker status
    docker stop/waiting
    $ service docker stop


    $ docker -H 192.168.99.50:2375 -d 
    put it on port 2375, standard non-SSL Docker port, -d to put it in daemon mode

    $ docker info
    Cannot connect to the Docker daemon, Is the docker daemon running on this host?

On CentOS
    change docker api client version to same with Ubuntu docker server. 
    $ export DOCKER_API_VERSION=1.21
    $ export DOCKER_HOST="tcp://192.168.99.50:2375"

    now check docker version
    $ docker version

## Playing Around with Our First Docker Container

$ docker run -it centos /bin/bash

after run docker centos then run bash.

    So, we can ping stuff, so Google's infamous DNS servers
    $ ping 8.8.8.8


    $ ps -elf

    $ cat /etc/hosts
    17.2.17.0.2      30cf3f4a78c

    17.2.17.0.2  is ip address
    30cf3f4a78c  is host name


    $ yum install net-tools

    $ ifconfig

    $ uname -a
    //showing linux version


    $ cat /etc/redhat-release
    CentOS Linum release 7.3.1611 (Core)

    // update package CentOS
    $ yum check-update

    exit container
    $ exit

$ docker ps -a 
container   30cf3f4a78cc

show containers images
root@ubuntu1404-05:/# ls -l /var/lib/docker/aufs/diff/
total 44
drwxr-xr-x  2 root root 4096 Aug 14 13:36 2af8dff0d004af887d2b8b92699af2211b010aa59547185e2baf753853cf0713
drwxr-xr-x 10 root root 4096 Aug 14 15:10 30cf3f4a78ccf378bc644e7988e9bc31f869610271f73f7f2cf8fb447c48ec5a
drwxr-xr-x  8 root root 4096 Aug 14 13:43 30cf3f4a78ccf378bc644e7988e9bc31f869610271f73f7f2cf8fb447c48ec5a-init
drwxr-xr-x  3 root root 4096 Aug 13 02:06 3216af24499532c2661760b8fd5c47bb75010470bf50a1cd64693c9ca1763ae4
drwxr-xr-x  6 root root 4096 Aug 13 02:06 3fb6ea6c6e20f1f828ef5d5d89d80991666f4afad8131873aacc68618443a143
drwxr-xr-x  3 root root 4096 Aug 13 02:06 4ae1232510d52f36167c4667525d68f65f33b9613a2139044aed5c5cb0cc0790
drwxr-xr-x  2 root root 4096 Aug 13 02:06 56a4fe6a7878a43f591155ed8f426ad857b452b1e42b83c0a702aab260b0efd3
drwxr-xr-x 21 root root 4096 Aug 13 02:06 9033d138d2abc3e7da07bda3ee589e7b03afa45fe0228a60a77c2aad4a1ae009
drwxr-xr-x  2 root root 4096 Aug 14 13:36 91c9b1b68791bd434376649a7aecefd72bdb1af9bd50599154c84e215f488ae0
drwxr-xr-x  3 root root 4096 Aug 13 02:06 e0a07d39927927e82a0a80096aaa4fbe77afaba40571c4983e474efe82785775
drwxr-xr-x 14 root root 4096 Aug 14 13:36 f08eab50aca8de994e69fe5465bba621f9aea980f2dfc6752812cc0ea21f1960
root@ubuntu1404-05:/# cat /var/lib/docker/aufs/diff/f08eab50aca8de994e69fe5465bba621f9aea980f2dfc6752812cc0ea21f1960/tmp/testfile

$ docker start 30cf3f4a78cc
$ docker attach 30cf3f4a78cc



# ================================================




# Docker Networking

## The docker0 Bridge

$ brctl show docker0



apt-get update && apt-get install -y iputils-ping traceroute apache2

# ===============================================

docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it -e ES_HEAP_SIZE="2g" -e LS_HEAP_SIZE="1g" -e LS_OPTS="--no-auto-reload" --name elk sebp/elk

docker run --restart always -p 5601:5601 -p 9200:9200 -p 5044:5044 -it -e MAX_MAP_COUNT="262144" --name elk sebp/elk

sysctl vm.max_map_count=262144

docker run --restart always --name jenkins -v $PWD/jenkins_home:/home/pichit/jenkins_home -d -p 8080:8080 -p 50000:50000 -it chenug/jenkins-dotnet:1.0

docker run --restart always --name jenkins -d -p 8080:8080 -p 50000:50000 chenug/jenkins-dotnet:1.0

bc4196fb1d6f46e48afe35aea889154f

c27120593d91

c27120593d91fb09826584d82613ef09d3d8050f974d90257123f246bd96d146

/var/lib/docker/vfs/dir/7be24e94846524681a70845334ca57e7f62990db336dc5877cb6f25ee7d13060


 install -d -g docker -m 2777 -v /var/jenkins_home

docker run -d --restart always --name sonarqube -p 9000:9000 -p 9092:9092 -it -e SONARQUBE_JDBC_USERNAME=sonar -e SONARQUBE_JDBC_PASSWORD=Tonhoam54 -e SONARQUBE_JDBC_URL=jdbc:postgresql://172.17.0.2:5432/sonar sonarqube

install postgres
 $ docker run --name postgres -p 5432:5432 -it -e POSTGRES_PASSWORD=Tonhoam54 -d postgres
172.17.0.22

after create postgres  docker then create new database 'sonar' for sonarqube


on host run
$ sysctl vm.max_map_count=100000000
 $ docker run -d --name sonarqube \
	-p 9000:9000 -p 9092:9092 \
	-e SONARQUBE_JDBC_USERNAME=tiksonar \
	-e SONARQUBE_JDBC_PASSWORD=Tonhoam54 \
	-e SONARQUBE_JDBC_URL=jdbc:postgresql://172.17.0.22:5432/sonar \
	sonarqube
docker run  -d --name sonarqube -p 9000:9000 -p 9092:9092 -it -e MAX_MAP_COUNT="100000000"  sonarqube

using this below
$ docker run  -d --name sonarqube -p 9000:9000 -p 9092:9092 -it -e MAX_MAP_COUNT="100000000" -e SONARQUBE_JDBC_USERNAME=sonar -e SONARQUBE_JDBC_PASSWORD=Tonhoam54 -e SONARQUBE_JDBC_URL=jdbc:postgresql://172.17.0.2:5432/sonar sonarqube
docker run  -d --name sonarqube -p 9000:9000 -p 9092:9092 -it -e SONARQUBE_JDBC_USERNAME=sonar -e SONARQUBE_JDBC_PASSWORD=Tonhoam54 -e SONARQUBE_JDBC_URL=jdbc:postgresql://172.17.0.2:5432/sonar sonarqube

On SonarQube FirstLogin

Generate a token
sripirom: 89fda151b2fb48a65a50d3746ae4e4322ffe6116
The token is used to identify you when an analysis is performed. If it has been compromised, you can revoke it at any point of time in your user account.

https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild

Sample C# project
Execute the SonarQube Scanner for MSBuild from your computer

Running a SonarQube analysis is straighforward. You just need to execute the following commands at the root of your solution.

SonarQube.Scanner.MSBuild.exe begin \
  /k:"tik-owinnancy" \
  /d:"sonar.host.url=http://35.194.215.123:9000 \
  /d:"sonar.login=89fda151b2fb48a65a50d3746ae4e4322ffe6116"
SonarQube.Scanner.MSBuild.exe begin -k:"tik-owinnancy" -d:"sonar.host.url=http://35.194.215.123:9000 -d:"sonar.login=89fda151b2fb48a65a50d3746ae4e4322ffe6116 -n:"tik-owinnancy" -v:"1.0"
SonarQube.Scanner.MSBuild.exe begin /k:"tik-owinnancy" /n:"tik-owinnancy" /v:"1.0"
Copy
MsBuild.exe /t:Rebuild
Copy
SonarQube.Scanner.MSBuild.exe end \
  /d:"sonar.login=89fda151b2fb48a65a50d3746ae4e4322ffe6116"

------------------------------------------------------

Sample build OSX
Execute the SonarQube Scanner from your computer

Running a SonarQube analysis is straighforward. You just need to execute the following commands in your project's folder.

sonar-scanner \
  -Dsonar.projectKey=tik-owinnancy \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://35.194.215.123:9000 \
  -Dsonar.login=89fda151b2fb48a65a50d3746ae4e4322ffe6116

------------------------------------------------------------
download sonarqube tool https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild
setting path target execute file MSBuild.SonarQube.Runner.exe
export PATH=$PATH:~/SripiromDev/Tools/sonar-scanner-msbuild



Postgres

$ docker -it exec containerId base

Step # 1: Add a Linux/UNIX user called tom
run on postgres container
$ adduser sonar
$ passwd Tonhoam54

Step # 2: Becoming a superuser
# su - postgres

Step #3: Now connect to database server
$ psql template1
OR
$ psql -d template1 -U postgres

Step #4: Add a user called tom
template1=# CREATE USER sonar WITH PASSWORD 'Tonhoam54';

Step #5: Add a database called sonar
template1=# CREATE DATABASE sonar;

template1=# GRANT ALL PRIVILEGES ON DATABASE sonar to sonar;

template1=# \q

Step #6: Test tom user login
$ su - sonar
$ psql -d sonar -U sonar






sudo curl -o /usr/local/bin/docker-compose -L "http://github.com/docker/compose/releases/download/1.15.0/docker-compose-$(uname -s)-$(uname -m)"

sudo chmod +x /usr/local/bin/docker-compose


docker-compose -f docker-compose.yml -f docker-compose.overide.yml run backup_db