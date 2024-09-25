# Docker in the real world
### Creating a docker file
```
FROM python:3.13-rc-alpine3.20

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . . 

LABEL maintainter = "junnel <junnel.arsenio@nabepero.co.jp>" \
      version = "1.0"

CMD flask run --host=0.0.0.0 --port=5000
```


`docker --help` - this returns back all the docker commands that we can run with docker CLI

**To build your docker file**
- `docker build image -t name .`
 
**To inspect a docker image**  
- `docker image inspect name`

**To remove a docker image**
- `docker image rm name` or `docker image rm imageID` 
- `-f` : Adding `-f` to `rm` bypasses the error that you will encounter when removing docker images with the same `image ID`

**To shows the list of built docker images**
- `docker image ls` 

### Clean Up
- `docker container ls` : List all containers.
- `docker container ls -a` : List all stopped containers.
- `docker system df` - Show disk space is being used by docker, append `-v` is verbose
- `docker image ls` - Shows all docker images, any image that has the `<none>` tag are dangling/unused images
- `docker system info` - Display information about docker installation
- `docker system prune` - Prunes all safe to delete images and containers, append `-f` to delete without needing to confirm it, `-a` is to delete all unused images.
- `docker stop name1 name2 name3` - Stop the containers in `name1`, `name2`, and `name3`.
- `docker stop $(docker container ls -a -q)` - Stops multiple containers especially on running more than 10 or more docker containers


## Live coding with volume
**run this on terminal**

`docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v "current directory":/app web1`

**this is what it looks like on my terminal**

`docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v C:\Users\jhade\Downloads\diveintodocker\diveintodocker\src\06-docker-in-the-real-world\03-creating-a-dockerfile-part-1:/app web1`
