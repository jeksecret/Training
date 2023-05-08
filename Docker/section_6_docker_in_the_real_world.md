# Insights on this Section
#### Linking Containers with Docker Networks:
> ###### creating docker image
```
docker image build -t web2 .
```
> ###### pulling down redis image
```
docker pull redis:3.2-alpine
```
> ###### checking networks
```
docker network inspect bridge
```
> ###### running redis container
```
docker container run --rm -itd -p 6379:6379 --name redis redis:3.2-alpine
```
> ###### run flask app
```
docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 --name web2 -v $PWD:/app web2
```
> ###### finding local ip address of the redis server
```
docker exec redis ifconfig

docker exec web2 ifconfig
```
> ###### ping address
```
docker exec web2 ping e.g. ip addres(127.0.0.1)
```
> ###### linking redis and web2
```
docker exec redis cat /etc/hosts

docker network create --driver bridge firstnetwork

docker container stop web2

docker container stop redis

docker container run --rm -itd -p 6379:6379 --name redis --net firstnetwork redis:3.2-alpine

docker container run --rm -itd -p 5000:5000 -e  FLASK_APP=app.py -e FLASK_DEBUG=1 --name web2 -v $PWD:/app --net firstnetwork web2

docker network inspect firstnetwork

docker exec web2 ping redis

docker exec -it redis redis-cli

KEYS *

INCRBY web2_counter 1000
```
> ###### stopping the two containers linking
```
docker container stop web2

docker container stop redis
```
#### Persisting data to your Docker Host
```
docker volume create web2_redis

docker volume ls

docker volume inspect web2_redis

docker container run --rm -itd -p 6379:6379 --name redis --net firstnetwork -v web2_redis:/data redis:3.2-alpine
```
