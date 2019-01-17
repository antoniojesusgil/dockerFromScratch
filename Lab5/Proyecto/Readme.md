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
