# DCA Pratical Guide:

## All teoric content from -> https://github.com/Evalle/DCA/blob/master/README.md

## Orchestration

* Init a swarm cluster

```$ docker swarm init --advertise-addr 192.168.0.18```

* Init a swarm cluster with autolock

```$ docker swarm init --autolock --advertise-addr 192.168.0.18```

* Get a token for manager nodes

```$ docker swarm join-token manager```

* Get a token for worker nodes

```$ docker swarm join-token worker```

* List all nodes in cluster

```$ docker node ls```

* Update cluster with autolock

```$ docker swarm update --autolock=true```

* List services

```$ docker service ls```

* Create a service

```$ docker service create --replicas 1 --name helloworld alpine ping docker.com```

* List ID, container name, docker image, node when is running, desired state, current state, last error and ports allocation

```$ docker service ps helloworld```

* List a full detail to a service

```$ docker service inspect --pretty helloworld```

* Remove a service

```$ docker service rm helloworld```

* Content - nginx-phpfpm.yml

```
version: '3'

services:
  nginx:
    image: nginx
    ports:
      - 8080:80
  php-fpm:
    image: bitnami/php-fpm
    ports:
      - 8081:80
```
* Deploy a stack

```$ docker stack deploy --compose-file nginx-phpfpm.yml mystack```

* List services running in stack

```$ docker stack services mystack```

* Filter a specific service in stack

```$ docker stack services --filter name=mystack_nginx mystack```

* Filter some services in stack

```$ docker stack services --filter name=mystack_nginx --filter name=mystack_php-fpm mystack```

* List ID, mode and replicas from stack

```$ docker stack services --format "{{.ID}}: {{.Mode}} {{.Replicas}}" mystack```

* List ID, name and replicas from stack

```$ docker stack services --format "ID: {{.ID}} Name: {{.Name}} Instances: {{.Replicas}}" mystack```

* Scale one service 

```$ docker service scale mystack_nginx=10```

* Scale two services in the same command 

```$ docker service scale mystack_php-fpm=5 helloworld=5```
