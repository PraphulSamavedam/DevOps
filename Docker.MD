# Docker
Docker - "Build, ship and deliver anywhere". 
Docker has 2 main components, namely _Image_ and _Container_.
+ _Image_ - Read only templates to create containers/template of the end product.
+ _Container_ - Run state of the image/ spinned up image which behaves independently.
Docker allows to run containers at ease. 

### Containerization vs Virtualization
Containerization is virtualization at OS level. Containers support only the host OS based containers i.e. 
windows containers can only be run on the windows host machine and linux based containers can only be run on the linux host machines.
Virtual machines allows to run the cross platform applications.As the virtual machines run over the hypervisor they can spin other OS 

## Docker Commands
Please ensure that you have the administrator preveileges while running the docker commands and virtualization is enabled.
* `docker ps`
This provides the list of the presently running jobs
* `docker ps -a`
This provides the complete list of the jobs included the terminated jobs.
* `docker pull <image_name` Brings the docker image to local system from the docker.io or the repository which has been added in the repository url in case the image is not already located locally.
To get the image name visit [Docker Official Page](https://hub.docker.com/) and search for the pull syntax.
    
    Incase a specfic version look for its tag and run to get the pull commands
* `docker pull <image_name>:<tag_id>` Fetches the tag version of the image
* `docker images` Lists the locally available images
* `docker run <image_name>:<tag_id>`  Creates a container of the image with random container name.
* `docker run -itd --name FirstInstance centos` Creates a container of centos with name FirstInstance. This container is created as interactive(-i), TTYL enabled(-t) and detached(-d) mode. Incase the `centos` image is not present locally docker will internally calls the first pulls the centos image and then creates the container.
* `docker stop <container_id>` Only stops the container does not remove the container, stores its contents does not remove them. 
* `docker rm <container_id>` This removes the container i.e. implicitly the container is first stopped and then removed. 
* `docker stop <docker_id> && docker rm <container_id>` Docker commands can be combined using && operation between commands. This is simply `docker rm <container_id>`as mentioned it implicitly stops the container.
* `docker exec -it <container_id> <command>` Runs the command on the container without requiring to explicitly login and run the script.
* `docker logs <log_id>` Displays the content of the log. 
* `docker inspect <image_id>:<tag_id/name>` Displays the contents of the image. 
* `docker cp <container_id>:<absolute_path_to_container> <absolute_path or realtive_path of host>` Copies the content from container to host machine at specified location.
* `docker cp <absolute_path or realtive_path of host> <container_id>:<absolute_path_to_container>` Copies the content from host machine to container machine at specified location.
* `docker run -itd -e <ENV_VARIABLE>=<ENV_VARIABLE_VALUE> <image>` Passing environment variables.As docker container cannot access the environment variables of the host machine the environment variables can be passed at the container creation as "-e"
Example: `docker run -d --name mysqlDB -e MY_SQL_ROOT_PASSWORD="helloworld" -e MY_SQL_DATABASE=dbtest mysql:8.0.17`
* `docker rmi <image_id>` Removes the image from local storage. Please ensure that no container is running with this image during the execution of this command. As this doesn't implicitly stop and remove the container running using this image.
* `docker prune` Unused images and containers are removed basedn on the inactivity.
* `docker run -d --name <Container_name> -p <host_port_id>:<container_port_id> <image_name>:<tag>` Portforwarding from container's default port to custom host's port. This is helpful when host machine has some service running on the default port of the container service port.
* `docker volume create <volume_name>` Creates a logical volume for the containers in the host machine.
* `docker volume inspect <volume_name>` To Inspect the created volume, especailly the mount point indicates where the volume is mounted on the host machine.
* `docker run -itd --name <container_name> -v <volumename>:<container_volume> <image_name>` Binds the host's logical volume to containers volume passed. Volumes can be shared by multiple containers thus resource utilization is possible.
* `docker network ls` Lists all the networks connected to Docker. The default network 'bridge'
* `docker network inspect <network_id>` Inspects the docker network. 
* `docker network create <network_name>` create a new network on the host machine system, starting with "br_"
* `docker run -itd --name <container_name> --net <network_name> <image_name>` Spins a container with name "container_name" on the network "network name". This is same as below command
* `docker run -itd --name <container_name> --network <network_name> <image_name>` Spins a container with name "container_name" on the network "network name". This is same as above command, inshort --net or --network mean the same.
* `docker build <Dockerfile> -t <image_tag_id>` creates the custom image based on the dockerfile.Some standard image tags has the following nomenclature 'repository-url/name:version' 
* `docker-compose -f <yaml_file> up --no-build -d` creates the container based on the yaml file without building the image as background process(*-d*). 'up' indicates that the container is spun up and running.
* `docker-compose -f <yaml_file> up` creates the container based on the yaml file by creating an image and container is up and running.
* `docker login <full_url_of_organization's_docker>` The default registry where docker looks is _[https://hub.docker.com/](https://hub.docker.com/)_. In order to overwrite this default this command adds the absolute url as the primary url.

**These are only few docker commands, More are available in the _[official docker documentation](https://docs.docker.com/)_. In case struck with any command and require help, type 'docker command --help'**

### Custom Image
As seen above, the custom images can be defined in 2 ways. 
1. Dockerfile
2. YAML based definition

##### 1.  Dockerfile
Dockerfile is built on the base images and some additional packages to run the code. Sample dockerfile is as follows:(sentence prefixed with # is a comment in Dockerfile)
```
FROM centos                 
# FROM <base_image> => Base image is taken for image creation
MAINTAINER "praphulsamavedam@gmail.com"  
# MAINTAINER <DL-email_name> =>  Maintainer indicates who maintains this custom image for reference, not mandatory but good practice.
WORKDIR /usr/bin 
# WORKDIR <absolute_path> => WORKDIR refers to working dir, this needs to be done for some images which have mandatory WORKDIR field.
RUN yum -y install git # Installs the required packages on the top of the base image. 
# RUN <command> => This is run during image creation, by add a layer over the existing image. Usually used to add necessary packages or softwares.
RUN yum -y install python 
# RUN <install_command> => This adds a layer over the existing image. 
COPY *.py ./
# COPY <source> <destination> => This is used to copy files from or to the container. Usually used to add the code repository for container.
CMD ["python","launch.py"]
# CMD [<binary>,<arg1>,<arg2>,...] => This is used to execute the binaries at the time of the container creation. Usually used to run the command at the container level, but is not converted into microservice.
ENTRYPOINT ["python","main.py"]
# ENTRYPOINT ["<binary>","<arg1>","<arg2>",...] =>This connverts the container to microservices and runs the binary with arguments. The container can be accessed only through montoring tools like splunk, docker logs,etc.
```

##### 2.  YAML based definition
YAMML means "YAML Ain't Markup Language" (a recursive acronym), is a human-readable data-serialization language. 
```
version: '3'

services:
    mysqldb:
        image: mysql:8.0.18
        command: --default-authentication-plugin=mysql_native_password
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: example
    
    adminer:
        image: adminer
        restart: always
        ports:
          - 9090:8080
```
This YAML has 2 services,    
1. DB service (mySQL db)
2. Adminer (HTML page based DB orchestrator)

Under every service, we can pass the values simultaneously and can also overwrite the default values if required. Like in this case the default value of 8080 od the adminer service has been overwritten with value of 9090. 
