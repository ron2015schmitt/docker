# Description 

This Dockerfile builds: 
- Ubuntu 
- curl
- nvm
- npm
- nodejs
- pnpm

The versions are called out in the file


# Build command
```bash 
../build 
```
Include option `--progress=plain` to print verbosely.
Include option `--no-cache` to clear your local docker build cache.

# Run commands


```bash
cd path-to-your-files
docker run -it --rm -v /"${PWD}":/home/user/work    node_pnpm
```

The option `-v /"${PWD}":/home/user/work` causes your files in the current directory to be *mounted* at `/home/user/work`` inside the container. Any changes made inside the container will change the files that are outside the container.

The option `-rm` deletes the image upon exit.

The option `-it` puts you in an interactive tty terminal.

Include option `-u 0` to have root access inside the container


To verify the versions beign used once inside the container, type

```bash
info
```



