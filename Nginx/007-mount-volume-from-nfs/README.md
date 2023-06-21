## Deploy the stack
```sh
docker stack deploy -c [path]/docker-compose.yaml [stack_name]
docker stack deploy -c docker-compose.yaml ee-001

docker stack deploy --compose-file [path]/docker-compose.yaml [stack_name]
docker stack deploy --compose-file docker-compose.yaml ee-001
```

## Reload nginx
```sh
docker service ls
docker ps |grep [service_name] | awk '{print "docker exec "  $1 " nginx -s reload"}' | bash
docker ps |grep ee-001_proxy | awk '{print "docker exec "  $1 " nginx -s reload"}' | bash
```

## Update the service
- pull the new image first
```sh
docker service update --image [image_repository] --update-delay 30s [service_name]
docker service update --image nginx:latest --update-delay 30s ee-001_proxy
```

## mime.types file example
https://github.com/nginx/nginx/blob/master/conf/mime.types