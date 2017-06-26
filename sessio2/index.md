# Sessio 2. Aplicació completa Node.js, Redis i NGiNX amb Docker




# Docker UI

[Portainer.io](https://portainer.io/)
Com a container:

```
docker run -d -p 9000:9000 portainer/portainer
```

Com a docker swarm:

```
docker swarm init

docker service create \
--name portainer \
--publish 9000:9000 \
--constraint 'node.role == manager' \
--mount type=bind,src=//var/run/docker.sock,dst=/var/run/docker.sock \
portainer/portainer \
-H unix:///var/run/docker.sock
```

# Docker Swarm

[!Tutorial configuració Docker Swarm](http://info.crunchydata.com/blog/easy-postgresql-cluster-recipe-using-docker-1.12)
[!Docker Compose to docker Swarm](https://codefresh.io/blog/deploy-docker-compose-v3-swarm-mode-cluster/)
