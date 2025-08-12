```shell
docker ps | grep my sql
```

you should see a container ID . now its time to login

```shell
docker exec -it f2b6d5df82b2 bash
```

If you want to remove the SQL container (Corrupted, health is down, etc.)
```shell
docker rm -f e9a84131d51b                                             
```