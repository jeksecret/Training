# Insights on this Section
#### Linking Containers with Docker Networks:
> ###### Building and Pushing Docker Images
```cmd
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
> ######
```
docker image build -t web2 .

docker image pull redis:3.2-alpine

docker network ls

ifconfig (MacOS / Linux)

ipconfig (Windows)

docker network inspect bridge

docker run --rm -itd -p 6379:6379 --name redis redis:3.2-alpine

docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py \
 -e FLASK_DEBUG=1 --name web2 -v $PWD:/app web2

docker exec redis ifconfig

docker exec web2 ifconfig

docker exec web2 ping 172.17.0.3

CTRL + C

docker exec redis cat /etc/hosts

docker container ls

docker network create --driver bridge firstnetwork

docker network inspect firstnetwork

docker container stop web2

docker container stop redis

docker container run --rm -itd -p 6379:6379 --name redis \
 --net firstnetwork redis:3.2-alpine

docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py \
 -e FLASK_DEBUG=1 --name web2 --net firstnetwork -v $PWD:/app web2

docker network inspect firstnetwork

docker exec web2 ping redis

docker exec -it redis redis-cli

KEYS *

INCRBY web2_counter 1000000

CTRL + D

docker container stop web2

docker container stop redis
```
> ###### Persisting Data to Your Docker Host
```
docker container run --rm -itd -p 6379:6379 --name redis \
 --net firstnetwork redis:3.2-alpine

docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py \
 -e FLASK_DEBUG=1 --name web2 --net firstnetwork -v $PWD:/app web2

docker container stop redis

docker container run --rm -itd -p 6379:6379 --name redis \
 --net firstnetwork redis:3.2-alpine

docker container stop redis

docker volume create web2_redis

docker volume ls

docker volume inspect web2_redis

docker container run --rm -itd -p 6379:6379 --name redis \
  --net firstnetwork -v web2_redis:/data redis:3.2-alpine

docker exec redis redis-cli SAVE

docker container stop redis

docker container stop web2
```
> ###### Sharing Data Between Containers
```
docker build -t web2 .

docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py \
  -e FLASK_DEBUG=1 --name web2 --net firstnetwork -v $PWD:/app web2

docker container run --rm -itd -p 6379:6379 --name redis \
  --net firstnetwork --volumes-from web2 redis:3.2-alpine

docker exec -it redis sh

cd /

ls -la

cat app/public/main.css

docker container stop web2

docker container stop redis

docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py \
  -e FLASK_DEBUG=1 --name web2 --net firstnetwork -v $PWD:/app -v /app/public web2

docker container run --rm -itd -p 6379:6379 --name redis \
  --net firstnetwork --volumes-from web2 redis:3.2-alpine

docker container exec redis cat /app/public/main.css

docker container stop web2

docker container stop redis
```
