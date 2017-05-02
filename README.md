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


