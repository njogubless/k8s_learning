if an app is composed of multiple apps,,
container for front-end
contaienr for backend
container for redis cache

its practical to deploy the app using one command  i.e docker compose

### Docker Compose
 - Define and run mutli-container applications
 - Define using YAML files
 - Run using the docker CLI with the compose plugin
    - Docker compose

### sample
```python

versrion: '3.9'

services:
  webapi1:
    image: academy.azurecr.io/webapi1
    ports:
      - '8081:80'
    restart: always

  webapi2:
     image: academy.azurecr.io/webapi2
     ports:
       - '8082:80'
    restart: always

  apigateway:
     image: academy.azurct.io/apigateway
     ports:
       - '80:80'
    restart: always
```

#### Docker compose cheat sheet

### Build the images
 `docker compose build`

### start the containers
 `docker compose start`

### stop the containers
 `docker compose stop`

### build and start
 `docker compose up -d`

### list what's running
` docker compose ps`
### remove from memory
` docker compose rm`

### stop and remove
`docker compose down`

### get the logs
` docker compose logs`

### Run a command in a container
` docker compose exec [container] bash`

### Run an instance as a project
`docker compose --project-name test1 up -d`

### shortcut
` docker compose -p test2 up -d`

### copy files from the container
` docker compose cp [ containerID]: [SRC_PATH] [ DEST_PATH]`
### copy files to the container
` [SRC_PATH] [ContainerID]: [DEST_PATH ]`
