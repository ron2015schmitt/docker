
# Docker 2023

Each subdirectory holds a different Dockerfile for various builds.

During the build process, the docker image is given the same name as the subdirectory housing the build file.


# Build command

```bash 
cd path-of-subdirectory
../build 
```

Include option `--progress=plain` to print verbosely.

Include option `--no-cache` to clear your local docker build cache.

# Run commands


```bash
cd path-to-your-files
docker run -it -v /"${PWD}":/home/user/work    docker-image-name
```

The option `-v /"${PWD}":/home/user/work` causes your files in the current directory to be *mounted* at `/home/user/work` inside the container. Any changes made inside the container will change the files that are outside the container.

The option `-it` puts you in an interactive tty terminal.

Include option `-name container-name` to give your container a name

Include option `-rm` to delete the container upon exit (and start anew the next time).

Include option `-u 0` to have root access inside the container

Include option `-p port_outside:port_inside` for each TCP/IP port that is needed.

Once inside the container, type the following to verify the versions of commands in use:

```bash
info
```


# Connecting to a Container with VS Code

https://code.visualstudio.com/docs/devcontainers/attach-container  

To attach to a Docker container, either 

- Step 1: Hit F1 by and type `Dev Containers: Attach to Running Container...` in the Command Palette

 
![image](https://github.com/ron2015schmitt/docker/assets/11559541/310d7f53-9b23-4077-a33d-760e16535896)

![image](https://github.com/ron2015schmitt/docker/assets/11559541/761bc60d-6030-42c2-a78f-657141d75d6d)


- or use the **Remote Explorer** in the **Activity Bar** and from the **Containers** view, select the **Attach to Container** inline action on the container you want to connect to.

