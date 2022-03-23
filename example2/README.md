# Dockerize a Python web app

## 1. Create the app locally 

```console
$ python3 -m venv venv
$ . venv/bin/activate
$ pip install fastapi uvicorn
```

Try it:

```console
$ uvicorn app.main:app --port 80
```

Save dependencies:

```console
$ pip freeze > requirements.txt
```

## 2. Build the Docker image

```console
$ docker build -t fastapi-image . 
```

Note that we use a `.dockerignore` file to ignore certain files/folders.

## 3. Run the Docker image

Normal:

```console
$ docker run -p 80:80 fastapi-image
```

Run in background and give a name:

```console
$ docker run -d --name myfastapicontainer -p 80:80 fastapi-image
```

`-p 80:80`: Map the port from outside to the port from the container

Host in Dockerfile must be:

`host: 0.0.0.0`: "placeholder", it tells a server to listen for and accept connections from any IP address ("all IPv4 addresses on the local machine").
