# Docker

## Cleanup

Reset/cleanup docker

```shell
docker-compose down
docker system prune
docker images prune
docker rmi -f $(docker images -aq) # remove all images
docker container prune

docker volume prune
docker restart
```
