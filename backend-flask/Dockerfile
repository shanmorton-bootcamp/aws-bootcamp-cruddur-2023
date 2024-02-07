FROM python:3.10-slim-buster

# Inside the container
# Make a new folder inside the container
WORKDIR /backend-flask

# copy files from outside the container to inside the container
# this contains the library we want to install, to run the app
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

# Inside the container
# run the libraries used for our app!
COPY . .

# Set EnvVars
# This is set INSIDE the container and remains set when the container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]