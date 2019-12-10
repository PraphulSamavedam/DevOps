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
* `docker stop <container_id>` Only stops the container does not remove the container, contains are not removed. 
* `docker rm <container_id>` This removes the container i.e. implicitly the container is first stopped and then removed. 
* `docker stop <docker_id> && docker rm <container_id>` Docker commands can be combined using && operation between commands. This is simply `docker rm <container_id>`as mentioned it implicitly stops the container.
* `docker exec -it <container_id> <command>` Runs the command on the container without requiring to explicitly login and run the script.
