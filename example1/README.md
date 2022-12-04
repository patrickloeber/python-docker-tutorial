# Dockerize a simple Python script with third-party modules

We differ between:

- Dockerfile: Blueprint for building images
- Image: Template for running containers
- Container: Running process with the packaged project

## 1. Build the Docker image

```console
$ docker build -t python-imdb . 
```

## 2. Run the Docker image (starts the container)

Without user input:

```console
$ docker run python-imdb
```

If you want user input (comment out the `break` in [main.py](./main.py)):

```console
$ docker run -t -i python-imdb
```

-i: interactive, -t: pseudo terminal
