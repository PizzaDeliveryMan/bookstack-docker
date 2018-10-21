## Docker Image For [BookStack](https://github.com/ssddanbrown/BookStack)

### Quickstart ----- WITH ---- Docker-Compose
With Docker Compose is a Quickstart very easy. Run the following command:

```
docker-compose up
```

and after that open your Browser and go to [http://localhost:8080](http://localhost:8080) .


### Installation ----- WITHOUT ----- Docker compose
Networking changed in Docker v1.9, so you need to do one of the following steps.

#### Docker < v1.9
1. MySQL Container:
```bash
docker run -d --name bookstack-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=bookstack -e MYSQL_USER=bookstack -e MYSQL_PASSWORD=secret mysql:5.7.21
```
2. BookStack Container:
```bash
docker run --name my-bookstack -d --link bookstack-mysql:mysql -p 8080:80 solidnerd/bookstack:0.24.1
```

#### Docker 1.9+

1.Create a shared network:

```bash
docker network create bookstack_nw`
```

2.MySQL container :
```bash
docker run -d --net bookstack_nw  \
-e MYSQL_ROOT_PASSWORD=secret \
-e MYSQL_DATABASE=bookstack \
-e MYSQL_USER=bookstack \
-e MYSQL_PASSWORD=secret \
 --name="bookstack_db" \
 mysql:5.7.21
```


3.Create BookStack Container

```bash
docker run -d --net bookstack_nw  \
-e DB_HOST=bookstack_db:3306 \
-e DB_DATABASE=bookstack \
-e DB_USERNAME=bookstack \
-e DB_PASSWORD=secret \
-p 8080:80 \
 solidnerd/bookstack:0.24.1
```

