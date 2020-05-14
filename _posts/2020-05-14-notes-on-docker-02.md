---
layout: post
title:  "Notes on Docker 02"
date:   2020-05-14 05:00:00 -0300
categories: [docker]
---
## Dockerfile commands.

Each instruction creates one layer:

- ```FROM``` - creates a layer from the Docker image.
- ```COPY``` - adds files from your Docker client’s current directory.
- ```RUN``` - shell form, the command is run in a shell, which by default is /bin/sh -c on Linux or cmd /S /C on Windows). ```RUN ["executable", "param1", "param2"]```  (exec form) The instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile..
- ```CMD``` - specifies what command to run within the container.

for more details check: [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
