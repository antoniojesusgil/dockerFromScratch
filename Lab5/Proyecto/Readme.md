## docker-compose

### Construir las imágenes
```docker
docker-compose -f docker-compose.yml build
```
### Lanzar infraestructura contenedores
```
docker-compose up
```
## Docker swarm

```
docker swarm init
Swarm initialized: current node (15p1bp4xjcchmkur4q5qbqhqx) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1hjhq1lbxygc6sd96q74mbz4unvj7gegmgxpd90i2ct1bn6pu2-8yz4c9r3bs38srtvqcnnm365d 192.168.65.3:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```
```sh
docker stack deploy --compose-file docker-stack.yml votos
Creating network votos_frontend
Creating network votos_default
Creating network votos_backend
Creating service votos_result
Creating service votos_worker
Creating service votos_visualizer
Creating service votos_redis
Creating service votos_db
Creating service votos_vote
```

```
docker stack ls
NAME                SERVICES            ORCHESTRATOR
votos               6                   Swarm
```

### Iniciar los servicios

```
docker stack services votos
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
5tu0mh9iptef        votos_redis         replicated          1/1                 redis:alpine
j8hblzhcbwqu        votos_result        replicated          0/1                 resultado:before    *:5001->80/tcp
kf3lvne9e906        votos_vote          replicated          0/2                 voto:before         *:5000->80/tcp
kxopxg2w2c6d        votos_visualizer    replicated          0/1                 visualizer:stable   *:8080->8080/tcp
r3kfzbcjyz1j        votos_worker        replicated          0/1                 worker:latest
svcsfvnphfba        votos_db            replicated          1/1                 postgres:9.4

```
### Escalar
Incrementamos a 5 nodos
```
docker service scale voting_stack_vote=5
```
Comprobamos los nodos
```
docker service ps votos
```
Decrementar a 3 nodos
```
docker service scale voting_stack_vote=3
```


