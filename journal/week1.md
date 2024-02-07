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