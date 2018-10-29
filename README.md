# Demo of docker-compose issue with --project-directory

This demo relates to changes introduced by https://github.com/docker/compose/pull/6134

The understanding is that `--project-directory` will allow you run start up a docker-compose from another directory by specifying the 'project directory'. The understanding is that it will also load the `.env` file within that directory.

This pull request is only included in the latest release so ensure you're using docker-compose from https://github.com/docker/compose/releases/tag/1.23.0-rc3.


## Demo 1
* Run `docker-compose --project-directory docker up` from the root of the project

### Expected behaviour
The docker container is started using the `.env` file.

### Actual behaviour
```
ERROR:
        Can't find a suitable configuration file in this directory or any
        parent. Are you in the right directory?

        Supported filenames: docker-compose.yml, docker-compose.yaml
```

## Demo 2
* Run `docker-compose --project-directory docker -f docker/docker-compose.yml up` from the root of the project

### Expected behaviour
The docker container is started using the `.env` file.

### Actual behaviour
```
ERROR:
WARNING: The TAG variable is not set. Defaulting to a blank string.
ERROR: no such image: java:: invalid reference format
```

## Working example
* Run `docker-compose --project-directory docker config` from the root of the project

## Result
```
services:
  java:
    command: java -version
    image: java:alpine
version: '3.1'
```