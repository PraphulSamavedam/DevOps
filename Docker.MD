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
* `docker run -d --name <Container_name> -p <host_port_id>:<container_port_id>`

