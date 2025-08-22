### structure of a docker file
```python
 FROM alpine
 RUN APK add -update nodejs nodejs-npm
 COPY ./src
 WORKDIR /src
 RUN npm install
 EXPOSE 8080
 ENTRYPOINT ["NODE", "./APP.JS"]
```

- Base Image
- Install Node and NPM using the package manager
- copy the files from the build context
- working directory
- Run a command
- Adds metadata 
- what to run

### Containers are ephemerous and stateless
- Data is not stored in containers
- Data is not persistent in containers
      - locally on a writable layer
      - Its the default, just write to the filesystem
      - when containers are destroyed, so is the data inside them
#### ephemerous means = shortlived