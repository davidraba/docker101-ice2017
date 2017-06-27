# Sessio 2. Interconnexionat de containers

## Docker Compose

```
docker-compose up
```

```
docker-compose up -d 
```

```
docker-compose down
```

```
docker-compose up --force-recreate
```

##Aplicació completa Node.js, Redis i NGiNX amb Docker

* [Pas 1 - Node.js + Redis](simple)
* [Pas 2 - Node.js + Redis amb volum a host](simple-amb-volumes)
* [Pas 3 - NGiNX + Node.js + Redis](lb-simple)
* [Pas 4 - NGiNX + X Node.js + Redis](amb-volumes)

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

Si voleu explorar la utilització de Docker Swarm per fer deploy de bases de dades un molt bon article de referencia es aquest:
[Tutorial configuració Docker Swarm](http://info.crunchydata.com/blog/easy-postgresql-cluster-recipe-using-docker-1.12)

I pel que fa a la revisió de docker compose v3, que facilita molt la feina de dimensionar la arquitectura i la conversió a docker swarm:
[Docker Compose to docker Swarm](https://codefresh.io/blog/deploy-docker-compose-v3-swarm-mode-cluster/)

