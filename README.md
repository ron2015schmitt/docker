
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


# git set up

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Do not use option `-rm` in `docker run` command if you want the git info to persist.


# Connecting to a Container with VS Code

https://code.visualstudio.com/docs/devcontainers/attach-container  

To attach to a Docker container, either 

- Step 1: Hit F1 by and type `Dev Containers: Attach to Running Container...` in the Command Palette

 
![image](https://github.com/ron2015schmitt/docker/assets/11559541/310d7f53-9b23-4077-a33d-760e16535896)

![image](https://github.com/ron2015schmitt/docker/assets/11559541/761bc60d-6030-42c2-a78f-657141d75d6d)


- or use the **Remote Explorer** in the **Activity Bar** and from the **Containers** view, select the **Attach to Container** inline action on the container you want to connect to.
- 


# pnpm

https://pnpm.io/package_json 


# Angular projects

By default, Angular needs that you have git and git credentials set up because it sets up a git project.  However, it's best to include the option `--skip-git` during ng project creation and use git outside the container.

Include option `-p 4200:4200` in `docker run` command so that `ng serve` works.

Also make sure that `EXPOSE 4200` is included in the Dockerfile.

Keep in mind that the first time you run `ng serve` inside a project takes a very long time, >10 minutes. (unless you use new esbuild/vite builder).

Refer to [sample-angular-project](https://github.com/ron2015schmitt/sample-angular-project/tree/main#how-this-repo-was-created) for Angular installation notes.


# React Projects

Include option `-p 5173:5173` in `docker run` command so that `pnpm run dev` works.

Also make sure that `EXPOSE 5173` is included in the Dockerfile.

Refer to [sample-angular-project](https://github.com/ron2015schmitt/sample-react-project/blob/main/README.md#how-this-repo-was-created) for React installation notes.




