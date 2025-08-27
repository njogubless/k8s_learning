#### create volume
`docker volume create myvol`

#### inspect the volume
`docker volume inspect myvol`

#### list the volumes
`docker volume ls`

#### delete volume
`docker volume rm myvol`

#### delete all volumes not mounted
`docker volume prune`

#### run a container with a volume
`docker run -d --name devtest -v myvol:app nginx:latest`

when using the inspect volume command
#### docker inspect devtest
```python
[
    {
         "CreatedAt": "2025-08-27T10:11:19+03:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/myvol/_data",
        "Name": "myvol",
        "Options": null,
        "Scope": "local"

    }
]
```
instead of using a volume,, you can specify a local folder

#### runninf a container with a specified volume local folder
`docker run -d --name devtest -v d:/test:/app nginx:latest`

#### insepct the container

docker inspect devtest

```python
"Mounts":[
    {
       "Type":"bind",
       "Source":"/host_mnt/d/test",
       "Destination":"/app",
       "Mode":"",
       "RW":true,
       "propagation":"rprivate"

    }
]
```