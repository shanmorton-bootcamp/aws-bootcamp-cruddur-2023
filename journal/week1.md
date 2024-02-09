# Week 1 — App Containerization

I'm going through this bootcamp, again, on my own. 

I am STUCK in desktop support and I need to move up and out.
I think this will help me do that!

## Week 1 — App Containerization
https://www.youtube.com/watch?v=zJnNe5Nv4tE&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=19

Starting again!  Here we go!!

### New Dockerfile in backend-flask directory

We'll create a new docker file for the backend part of our project

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

After creating the docker file name making some notes,
I ran the requirments.txt file to install some needed libraries.

then ran the cmdn to run the docker container, to get the port started/open

``` 
python3 -m flask run --host=0.0.0.0 --port=4567

```

Stop the server by pressing Contol_C

Set some ENV Vars in the backend-flask folder

``` export FRONTEND_URL="*"
export BACKEND_URL="*"
```
Then restart the server w/ the command python3 cmd above.

Once the port becomes open and you make it public,

Open a webpage and go to 
https://4567-shanmortonb-awsbootcamp-fk60w0nkizn.ws-us108.gitpod.io/api/activities/home
and you'll see Data come back.


[PortOpenGettingData.jpg]


Unset the env var for Frontend and backend URLs

``` 
unset FRONTEND_URL
unset BACKEND_URL

```
Do make sure you are not in the backend-flask folder when you run the next command to build the docker image.

``` 
cd ../
docker build -t  backend-flask ./backend-flask

```

This work laptop is SO SLOW I'll have to go back to my own personal laptop to make this work.  Ugh!!!

02/08/12
I was able to move to my own laptop that is much better quality and faster than my work laptop.

I built the docker image and now I'll run the image/container using this cmd:

```
docker container run --rm -p 4567:4567 -d backend-flask
```
and I'll see it being active in side the docker panel.

Run this docker cmd and set some ENV Vars:
```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask

```

Now to set up the FrontEnd @ 1:43:43 in Week 1 — App Containerization video

Move to the Frontend folder and run an ``` npm i ``` to install node.

Create a new file named Docker file in the frontend directory. 

```
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm i
EXPOSE ${PORT}
CMD ["npm", "start"]

```

Created a new file in the root of my project, docker-compose.yml

```

version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./frontend-react-js
    ports:
      - "3000:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js

# the name flag is a hack to change the default prepend folder
# name when outputting the image names
networks: 
  internal-network:
    driver: bridge
    name: cruddur

```

You can run a "docker compose up" if you right click on the file.  There are several options for action there as well.
