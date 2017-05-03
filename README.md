# psgsdockerswarmmode

## 2. Why Multiple Container Hosts?
### 4 What if a Single Container isn't Enough?
```
docker run -d -p 3000:3000 swarmgs/nodewebstress
```
stress test
```
ab -n 100 http://127.0.0.1:3000/customer/1
```

parallel test
```
echo "http://127.0.0.1:3000/customer/1\http://127.0.0.1:3001/customer/2" | parallel -j 2 "ab -n 100 {.}"
```
## 3.Creating a Swarm and Running a a Service
### 3 Enabling Swarm Mode by Initializing a new Swarm
```
docker swarm -h
```
### 4 Listing and Inspecting Nodes
```
docker node ls
docker node inspect self
```

### 5 Creating an Nginx Service
```
docker service create --name web --publish 8080:80 nginx
```

### 7 Services Lead to Tasks
```
docker service ls
docker service ps web
```

### 8 Removing a Service
```
docker service rm web
```
### 9 Updating a Service to Scale the Number of Containers
make 2 containers(not make 2 more containers)
```
docker service ps web
docker service update --replicas=2 web
```
scale
```
docker service scale web=4
```
### 10 Swarm Managers Ensure the Desired State Is Maintained
```
docker stop 123
```

## 4. Adding Nodes
### 2 Destroying the Single Node Swarm
```
docker swarm leave --force
```

### 7  docker swarm init --advertise-addr
```
 docker swarm init --advertise-addr ip
 
 ```
### 8 Joining Worker Nodes to the Swarm Mode

```
docker swarm join-token worker
docker swarm join-token manager
```
### 9 Creating a Service to Visualize Our Cluster State
```
docker service create --name viz --publish 8090:8080 --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock --constraint=node.role==manager manomarks/visualizer
```

```
docker service ls
docker service ps viz
```
## 10 What Happens When a Node Is Shut Down
```
docker node rm -f c
```
## 16 Promoting a Worker to a Manager
```
docker node promote worker1
docker node demote manager1
```


## 11. Protecting Secrets
###

```
vi mysql.yml
```
edit
```
version: '3.1'
services:
  mysql:
    image: mysql
    environment:
      MYSQL_USER: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_ROOT_PASSWORD: root
    deploy:
      placement:
        constraints:
          - node.role==manager

```
docker stack deploy -c mysql.yml mysql
docker ps
docker exec -it 12345678 bash
```

```
mysql -uroot -p
show databases;
```


