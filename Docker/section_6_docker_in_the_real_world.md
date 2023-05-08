# Insights on this Section
#### Linking Containers with Docker Networks:
> ###### Building and Pushing Docker Images
```
docker --help

docker image --help

docker image build -t web1 .

docker image inspect web1

docker image build -t web1:1.0 .

docker image ls

docker image rm web1:1.0

docker image ls

docker login

docker image tag web1 nickjj/web1:latest

docker image ls

docker image push nickjj/web1

docker image rm -f [image id]

docker image ls

docker pull nickjj/web1

docker image ls
```
> ###### Running Docker Containers
```
docker image tag nickjj/web1 web1

docker image rm nickjj/web1

docker image ls

docker container ls

docker container run -it -p 5000:5000 -e FLASK_APP=app.py web1

docker container ls

CTRL + C

docker container ls -a

docker container rm [container id]

docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
 --rm --name web1 web1

CTRL + C

docker container ls -a

docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
 --rm --name web1 -d web1

docker container logs web1

docker container logs -f web1

CTRL + C

docker container stats

CTRL + C

docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
 --rm --name web1 -d web1

docker container run -it -p 5000 -e FLASK_APP=app.py \
 --rm --name web1_2 -d web1

docker container ls

docker container run -it -p 5000 -e FLASK_APP=app.py \
 --rm --name web1_2 -d --restart on-failure web1

docker container run -it -p 5000 -e FLASK_APP=app.py \
 --name web1_3 -d --restart on-failure web1

docker container ls

docker container stop web1

docker container stop web1_2

docker container stop web1_3

docker container run --help
```
> ###### Live Code Reloading With Volumes
```
docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
  --rm --name web1 web1

CTRL + C

docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
  -e FLASK_DEBUG=1 --rm --name web1 web1

CTRL + C

docker image build -t web1 .

docker container run -it -p 5000:5000 -e FLASK_APP=app.py \
  -e FLASK_DEBUG=1 --rm --name web1 -v $PWD:/app web1

docker container inspect web1
```
