# Introduction to Docker for data science. 


## What is Docker? 
Docker is a set of platform as a service (PaaS) products that use 
OS-level virtualization to deliver software in packages called containers.

In short, docker can froozen your analytical environment including 
programming lauguage (R, Python or Julia) and packages. 

## Quickstart.
Move to `src_quickstart` and type `docker compose up`. 

Copy and paste url or Ctl + click url, and you can access Jupyter Lab
with R, Python, Julia environemtns.  
Url is like 
`http://localhost:8888/?token=123456789123456789123456789123456789`

## Basic flow of Docker. 
In docker system, you frequently manage images and containers. 
Docker image contains the froozen environment, which includes platforms 
such as programming laungage itself (R, Python, Julia), JupyterLab, packages.
The image is immutable object, so you can only use the image for read-only purpose.  
Docker container is mutable object and unfroozens a Docker image. 
You can begin to work on the container. 
To create a Docker image, you have to prepare dockerfile, and if you mange the whole flow 
of launching up docker environment, it's better to prepare docker-compose.yml file. 

You can gain a better understanding with a metapher. 
When you are a chef in a instant restaurant, you have to first prepare 
frozen food (Docker image) before opening a restaurant. 
So what you have to do is first create a recipe (Dockerfile) for frozen food. 
After preparing your froozen food, you will serve your food to customers. 
Then, the food is unfroozend and becomes a good hot food (Docker container), 
and you will serve this food to customers. 
In this restaurant, a chef will manage the whole flow of restaurant managemnet, and 
then a chef can be regarded as a docker-compose.yml.

Since the command `docker compose up` contains multiple steps, 
let's see how each step works in the following section.

## Explore what is happening after `docker compose up`.
We will continue to use the instant restaurant metaphar in the previous section, and 
use the directory `src_quickstart`.
To manage your restaurant, first a recipe is necessary.
In `src_quickstart/Dockerfile`, you can find `From jupyter/datascience-notebook:lab-3.6.3`. 
This line represents to use already prepared images uploaded to the web (DockerHub). 
This image managed by Jupyter already includes JupyterLab, R, Python, Julia environments, 
so you can easily use those languages instantly. 

To manually conduct this image building process, type 
`docker build -f Dockerfile -t test:v01 .`, creating `test:v01` image based on `Dockerfile`.
The current images installed in your PC can be checked by `docker image ls`.

In the next step, you need to unfroozen this image to be mutable objects, 
that is, to (launch docker container).
Type 
`docker run -it -p 8888:8888 --name test_container test:v01`. 
In this code, `test:v01` represents the docker image name.  
You can see the same url appeared after typing `docker compose up`, 
and you can work on this JupyterLab again.
Escape your environment by typing `Ctrl + c` in your terminal. 
You can check the current working container by `docker container ls` 
(maybe you can see nothign), and the existing container by `docker container ls -a`.

You notice that you have to type many commands to launch up container, 
which is annoying so much, and no reproducibility. 
Therefore, docker-compose.yml has a function to automate these process in an explicit file format. 
In `docker-compose.yml`, you can find container name, dockerfile specification, 
how to start up container, or etc... 

After preparing this file, `docker compose up` works as follows.
- If image is not existed, create an image based on `build` statement.  
- If container is not existed, create an container. 
- Launch a container based on the settings written in `docker-compose.yml`.

You have to notice "if statement" in the launchment process. 
For example, once you launch a container, even though `Dockerfile` is edited, 
`docker compose up` will re-launch the container based on the old docker image, 
since your docker image is not updated just by editing your `Dockerfile`. 
We will see how to solve this problem later.

It is good to see the internal file structure of container at this stage.
Type `docker start test_container` to run the docker container.
You can check container is running by `docker container ls`.
Type `docker container exec -it test_container bash` which enables you
to work in bash in the container.
Move to the root directory by `cd /` and type `ls`. 
The directory structure is very similar to the general OS structure, 
meaning that each docker engines run the process containing 
files in the general Linux OS system.  
You can escape from the container by `Ctrl + D`.

## Volume setting.
If you want to share the local directries with Docker container, 
you have to use volumes appropriately.   
In the `src_quickstart`, we share the local directry `.` with `workdir`.
In the `Dockerfile`, you create and move to `workdir` by the command `WORKDIR /workdir`, 
which enables you to first see the local content in the directry.

## Frequently used commands.

- `docker compose up`: Highly automated process from creating images 
and launching the container.

- `docker compose build`: After you edit the `Dockerfile`, type this command to 
create a new docker image.

- `docker image ls`: Look at the existing docker images.
- `docker container ls -a`: Look at the existing docker containers.
- `docker image prune`: Delete unnecessary docker images.
- `docker container prune`: Delete not running containers. 
- `docker container exec -it <container_name> bash`: Enter the container in bash.

## Practical usage.
- [Python packages](./src_Python_example/README.md)
- [R packages](./src_R_example/README.md)
- [Julia packages](./src_Julia_example/README.md)
- [PyMC4](./src_pymc4/README.md)
- [Webdav for zotero](./src_zotero/README.md)

## Searching tips for effectively using Docker.

## Selecting Image.
For the datascience purpose, it is highly recommended to use the jupyter image.  
[Selecting an Image, Docker Stacks documentation](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html)
The diagram in the "Image Relationships" section depicts the build dependency tree of
the core images. 

For R users, the rocker project is one option.

## Where is docker image stored? 
Type `docker info` and see the information related docker. 
You can find directory storing image in the line `Docker Root Dir`, 
so specifically type `docker info | grep "Docker Root Dir"`.   
If you are a linux user, you can check disk size docker is using by "Disk Usage Analyzer". 
You need a sudo permission to investigate docker file structure.
Launch the "Disk Usage Analyzer" by `sudo baobab`.

Or if you want to quickly check the directory size, use `sudo du -hs /var/lib/docker` for example.


## What is a difference between Docker and Virtual Machine. 
Virtual Machine launches the Guest OS on the host OS whereas 
Docker launches the Docker engine on the Host OS.  
Docker engine is one process. Process handles various applications such as 
web browser, sns tools, or microsoft Office. 
So the main advantage of docker over Virutual Machine is a light behaviour 
and managing multiple virtual environment (since a docker manages each process).





