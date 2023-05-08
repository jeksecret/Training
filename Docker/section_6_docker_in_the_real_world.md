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
docker exec web2 ping e.g.(127.0.0.1)
```
