# Dockerize a simple Python script with third-party modules

## 1. Build the Docker image

```console
$ docker build -t python-imdb . 
```

## 2. Run the Docker image

Without user input:

```console
$ docker run python-imdb
```

If you want user input (comment out the `break` in [main.py](./main.py)):

```console
$ docker run -t -i python-imdb
```

-i: interactive, -t: pseudo terminal
