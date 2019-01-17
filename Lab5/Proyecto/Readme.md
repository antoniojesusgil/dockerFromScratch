## docker-compose

### Construir las imágenes
```bash
docker-compose -f docker-compose.yml build
```
### Comprobar las imágenes
```bash
$ docker images                                                            
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
ajgil/resultado              latest              0d30ccf70113        4 days ago          80.7MB
ajgil/voto                   latest              ebd4e52b868b        4 days ago          70.9MB
ajgil/worker                 latest              214674010742        4 days ago          1.72GB
postgres                     9.4                 f66cb3765ad7        6 days ago          225MB
redis                        alpine              b42dc832c855        3 weeks ago         40.9MB
python                       2.7-alpine          66c225e226f9        3 weeks ago         58.3MB
```

### Lanzar infraestructura contenedores

Para probar el funcionamiento completo
```
docker-compose up
```

## Docker Swarm

```
What is Docker Swarm? 
Docker Swarm is a clustering and scheduling tool for Docker containers.
```
Caracteristicas mas importantes:

Networking trasnparente mediante redes distribuidas entre los nodos del cluster y los contenedores que se ejecutan en esos nodos.
Monitoriza el estado de los servicios volviendo a desplegar contenedores en caso caída. 

### Iniciar nodo Sarm

```
docker swarm init
Swarm initialized: current node (15p1bp4xjcchmkur4q5qbqhqx) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1hjhq1lbxygc6sd96q74mbz4unvj7gegmgxpd90i2ct1bn6pu2-8yz4c9r3bs38srtvqcnnm365d 192.168.65.3:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```
### Desplegar infraestructura 

```sh
$ docker stack deploy --compose-file docker-stack.yml stack-votos         
Creating network stack-votos_frontend
Creating network stack-votos_backend
Creating network stack-votos_default
Creating service stack-votos_vote
Creating service stack-votos_result
Creating service stack-votos_worker
Creating service stack-votos_visualizer
Creating service stack-votos_redis
Creating service stack-votos_db
```



### Iniciar los servicios

```
$ docker stack services stack-votos                                     
ID                  NAME                     MODE                REPLICAS            IMAGE                    PORTS
8ubza9g3xb2i        stack-votos_result       replicated          1/1                 ajgil/resultado:latest   *:5001->80/tcp
alwjqwia582u        stack-votos_vote         replicated          2/2                 ajgil/voto:latest        *:5000->80/tcp
k3vpchfhxqs1        stack-votos_redis        replicated          1/1                 redis:alpine
nfoot7s097pj        stack-votos_visualizer   replicated          0/1                 visualizer:stable        *:8080->8080/tcp
pc9pi5e2ty72        stack-votos_worker       replicated          1/1                 ajgil/worker:latest
sebpneytejts        stack-votos_db           replicated          1/1                 postgres:9.4
```
Comprobamos servicios
```
$ docker stack ls                                                         
NAME                SERVICES
stack-votos          6
```
Comprobar la infraestructura

### Escalar servicios

Incrementamos a 5 nodos el servicio de votos
```
$ docker service scale stack-votos_vote=5                                  
stack-votos_vote scaled to 5
overall progress: 5 out of 5 tasks
1/5: running   [==================================================>]
2/5: running   [==================================================>]
3/5: running   [==================================================>]
4/5: running   [==================================================>]
5/5: running   [==================================================>]
verify: Service converged
```
Comprobamos los nodos
```
$ docker service ps stack-votos_vote                                     
ID                  NAME                 IMAGE               NODE                    DESIRED STATE       CURRENT STATE                ERROR               PORTS
tdwgfbnta1fb        stack-votos_vote.1   ajgil/voto:latest   linuxkit-025000000001   Running             Running 5 minutes ago
t217s6tqgwnv        stack-votos_vote.2   ajgil/voto:latest   linuxkit-025000000001   Running             Running 5 minutes ago
w83s93pudgjh        stack-votos_vote.3   ajgil/voto:latest   linuxkit-025000000001   Running             Running about a minute ago
o7760xuh07e8        stack-votos_vote.4   ajgil/voto:latest   linuxkit-025000000001   Running             Running about a minute ago
i6wrfpmsjdso        stack-votos_vote.5   ajgil/voto:latest   linuxkit-025000000001   Running             Running about a minute ago
```
Decrementar a 3 nodos
```
$ docker service scale stack-votos_vote=3                                  
stack-votos_vote scaled to 3
overall progress: 3 out of 3 tasks
1/3: running   [==================================================>]
2/3: running   [==================================================>]
3/3: running   [==================================================>]
verify: Service converged
```


