# Week 1 — App Containerization

## Build container for Frontend

Create a docker file with the name "Dockerfile" this is the official name for any docker file. The dockerfile contains instructions to build the images by first pulling them from the registry then navigating the directory to copy and install the files.

```
FROM python:3.10-slim-buster

WORKDIR /backend-flask

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```

the meaning of the commands written in the file is as explained below
the
'FROM' is for telling us which image to pull from the registry
'RUN' is an image build step command
A Dockerfile can have many RUN steps that layer on top of one another to build the image.

'WORKDIR' shows us the working directory which we want to work from
'copy' is where we want to copy a file from the host system into the image using the syntax

> `COPY <SRC> <DEST>`

'ENV' set environment variables and
'EXPOSE' gives the post that should be exposed
'CMD' is the command which will execute by default at the end when you launch the build image

then we run the command

> `docker build -t backend-flask ./backend-flask`

'-t' is for tagging the image (naming it since it would give it the name latest if its not named)
after moving into the directory where the backend-flask folder is contained

this would build the image we can then run the container using

> ` docker run --rm -p 4567:4567 -it backend-flask`

--rm removes the previous container if its still running and -p gives the port which we want to expose
we can set the environment variables from the command above using the example

> `-e Frontend = '*' -e backend = '*'`

We would also do the same for the frontend part of the project

To can stand two containers at the same time using

> `docker-Compose  up`

command and

> `docker-Compose  down`

for shutting them down at the same time

## Connecting and fixing the notification route

The backend route is created using flask python and the data which we use is static

So we create a new service named notification_activities.py which returns a result, import it into the app.py file and create a new route which we can access from the frontend application.

We implement the request on the frontend application and then fix the route names and link
