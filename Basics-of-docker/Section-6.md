# Docker in the real world
### Creating a docker file
```
FROM python:3.13-rc-alpine3.20

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . . 

LABEL maintainter = "Abner <abner.masong@nabepero.co.jp>" \
      version = "1.0"

CMD flask run --host=0.0.0.0 --port=5000
```


`docker --help` - this returns back all the docker commands that we can run with docker CLI

