
# Description 

Each subdirectory holds a different Dockerfile for various builds.

The docker image is given the same name as the subdirectory housing the build file.


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

The option `-v /"${PWD}":/home/user/work` causes your files in the current directory to be *mounted* at `/home/user/work`` inside the container. Any changes made inside the container will change the files that are outside the container.

The option `-it` puts you in an interactive tty terminal.

Include the option `-rm` deletes the container upon exit (and start anew the next time).

Include option `-u 0` to have root access inside the container

Include option `-name container-name` to give your container a name


To verify the versions beign used once inside the container, type

```bash
info
```


# git set up

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Do not use option `-rm` in `docker run` command if you want the git info to persist.



# Angular projects

Angular likes that you have git and git credentials set up.  Although it's best to use git outside the container.

Include option `-p 4200:4200` in `docker run` command so that `ng serve` works.

Also make sure that `EXPOSE 4200` is included in the Dockerfile.

Keep in mind that the first time you run `ng serve` inside a project takes a very long time, >10 minutes.


## npm
```bash
cd work  # <--- MAKE SURE TO DO THIS OR YOUR WORK WILL NOT BE SAVED
ng new project-name 
```

## pnpm
```bash
cd work  # <--- MAKE SURE TO DO THIS OR YOUR WORK WILL NOT BE SAVED
ng new sample-project --package-manager=pnpm
```

Serving content
```bash
ng serve --host 0.0.0.0 --disable-host-check
```




