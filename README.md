# psgsdockerswarmmode

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


