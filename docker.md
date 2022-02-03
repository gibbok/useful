# Docker

## Cleanup

Reset/cleanup docker

```shell
docker-compose down
docker rm -f $(docker ps -a -q) # stop all containers
docker system prune
docker images prune
docker rmi $(docker images -a -q) # remove images
docker rmi -f $(docker images -aq) # remove all images
docker container prune

docker volume prune
docker volume rm $(docker volume ls -q) # clean volumes
docker restart
```
