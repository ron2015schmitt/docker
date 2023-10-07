# Ubuntu + NodeJS Dockerbuild 2023 

This Dockerfile builds: 

Base
- Ubuntu 
- *ca-certificates
- *dos2unix
- *curl
- *vim

NodeJS
- nvm
- npm
- pnpm
- nodejs

The versions are called out in the file, except those denoted above with an asterisk in which case the latest version is used.



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





