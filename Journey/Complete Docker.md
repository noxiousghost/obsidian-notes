### Why Containerization
containerization involves building self sufficient software packages that perform consistently, regardless of the machines they run on. It's basically taking the snapshot of a machine,the file system and letting you use and deploy it as a construct.
- Everyone has different OS
- Steps to run a project can vary based on OS
- Extremely harder to keep track of dependencies as project grows
- What if there was a way to describe your projects configuration in a single file?
- What if that could be run in an isolated environment 
- Makes Local setup of OS projects a breeze
- Makes installing auxiliary services or DB easy.

### Docker
- Makes it easier to deploy containers
- Allows for container orchestration which makes deployment a breeze
- Docker has three parts: CLI, Engine, Registry (docker hub)

### Docker Images & Containers
A docker image behaves like a template from which consistent containers can be crated.If docker was a traditional virtual machine, the image could be linked to the ISO use to install your VM. This isn't a robust comparison, as Docker differs from VMs in terms of both concept and implementation, but it's a useful starting point nonetheless.

Consistent containers means that once the image is created, it can be run in any OS with same outcome. 

Images define the initial file system sate of new containers. They bundle your application's source code and its dependencies into a self-contained package that's ready to use with a container runtime. Within the image, file system content is represented as multiple independent layers. Unlike github, which only lets you deploy your codebase, docker images 

Images are like the ISO file of Ubuntu OS in a pen drive. Container is when we run that image or execute it.  

Normally when running a nodejs application in our local system, we'd do node index.js. But while running that same application, first we'd create a docker image and describe what else we need apart from the code itself like nodejs, DBs, file system. An image is slightly harder to create because it is an independent entity that contains all dependencies that a code needs to run. `docker build` command is used to create an image.

Container is simply running the image. We can create multiple containers from an image but we'd create an image just once. `docker run<image_id>` is the command to create a container of a image. 

We'd send or upload the image to the docker hub and other people can run that image in their machine. For that they'd have to pull the image and run it using `docker pull <image_name>` `docker run <image_name>` commands respectively. 

### Docker File

FROM <baseimage: version>
WORKDIR <where do you want to work on the project>
COPY . . // copy all files in this project to the workdir. things on the left is the source and on the right is the desitination. 
RUN <process to run the application>
EXPOSE <port that a container exposes to the outer computer>

CMD <This runs when you are running the container>

**Create an image from a docker file:**
- docker build . -t <tag_name> // this will pull the base image from docker hub, copy all the files, run installation commands
- docker run -p 3001:3000<image_name> // this will run the image and map the port 3000 of the image to 3001
- docker ps // shows the running containers. to show all containers that are not running use -a flag

> if the image of a codebase is already created and the the source code is modified but the external dependency is not then we need to cache external modules because npm install is an expensive process. 
> If a top layer is changed then (lets say we set FROM node: 20 to node:19) then all the below layers are not cached, everything need to be build from scratch. 


