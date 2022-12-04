# How to create a great local Python development environment with Docker

Work in progress

1. Why Docker?
2. Dockerize an app
3. Immediate file changes (volumes)
4. Use IDE in Docker
5. Docker Compose
6. Add more services (Redis)
7. Debug Python code inside a container

## 1. Why Docker?
Python versions, more than just a virtual env, ...
## 2. Dockerize an app

```Dockerfile
FROM python:3.10-slim
WORKDIR /code
COPY ./requirements.txt ./
RUN pip install --no-cache-dir --upgrade -r requirements.txt
COPY ./src ./src
CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "80", "--reload"]
```

Use `Dockerfile` and the code in scr directory

(Use slim or alpine for smaller versions)

```console
docker build -t fastapi-image .
docker run --name fastapi-container -p 80:80 fastapi-image
docker run -d --name fastapi-container -p 80:80 fastapi-image
```
## 3. Immediate file changes (volumes)

```console
 docker stop fastapi-container
 docker ps -a
 docker rm fastapi-container

 docker run -d --name fastapi-container -p 80:80 -v $(pwd):/code fastapi-image
 ```
## 4. Use IDE in Docker
## 5. Docker Compose

```yml
services:
  app:
    build: .
    container_name: python-server
    command: uvicorn src.main:app --host 0.0.0.0 --port 80 --reload
    ports:
      - 80:80
      - 5678:5678
    volumes:
      - .:/code
```

Use `docker-compose.yml`

```console
docker-compose up
docker-compose down
```

## 6. Add more services (Redis)

```yml
services:
  app:
    ...
    depends_on:
      - redis

  redis:
    image: redis:alpine
```
## 7. Debug Python code inside a container

Add this in the code

```python
import debugpy

debugpy.listen(("0.0.0.0", 5678))

# print("Waiting for client to attach...")
# debugpy.wait_for_client()
```

And the port in yml:

```yml
services:
  app:
    ...
    ports:
      - 80:80
      - 5678:5678
```

Attach to running container

 ## Try a Python version easily with Docker

```console
 docker pull python:3.11-slim
 docker run -d  -i --name python_dev python:3.11-slim
 docker exec -it python_dev /bin/sh
```

## Further Resources:

- https://towardsdatascience.com/debugging-for-dockerized-ml-applications-in-python-2f7dec30573d
- https://github.com/Wyntuition/try-python-flask-redis-docker-compose
- https://docs.docker.com/compose/gettingstarted/
- https://www.docker.com/blog/containerized-python-development-part-1/


## Other commands for cleaning up

```console
docker rm container_name
docker image rm image_name
docker system prune
docker images prune
```

Check folder size:

```console
du -sh *
```
