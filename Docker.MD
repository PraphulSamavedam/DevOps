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
* `docker pull <image_name>:<tag_id>` Fetches the tag version of the image.
* `docker images` Lists the locally available images


