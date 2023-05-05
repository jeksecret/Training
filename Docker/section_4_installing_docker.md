# Insights on this Section
installing docker desktop https://www.docker.com/
#### Docker Desktop:
- enables you to build and share containerized applications and microservices.
- creates a VMs using that hypervisor that is running native js.

#### Verifying if Docker is installed:
`commands`
```
docker info

docker-compose --version
```
#### Docker Desktop requires a newer WSL kernel version.
```
wsl --update
wsl --set-default-version 2
```
