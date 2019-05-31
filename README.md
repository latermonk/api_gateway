# API- Gateway




## KONG
https://konghq.com/kong/  

### 安装kong
https://docs.konghq.com/install/docker/


```
docker network create kong-net


docker run -d --name kong-database \ --network=kong-net \ -p 5432:5432 \ -e "POSTGRES_USER=kong"  \ -e "POSTGRES_DB=kong"  \ postgres:9.6


docker run --rm \ --network=kong-net \ -e "KONG_DATABASE=postgres"  \ -e "KONG_PG_HOST=kong-database"  \ -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database"  \ kong:latest kong migrations bootstrap


docker run -d --name kong \ --network=kong-net \ -e "KONG_DATABASE=postgres"  \ -e "KONG_PG_HOST=kong-database"  \ -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database"  \ -e "KONG_PROXY_ACCESS_LOG=/dev/stdout"  \ -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout"  \ -e "KONG_PROXY_ERROR_LOG=/dev/stderr"  \ -e "KONG_ADMIN_ERROR_LOG=/dev/stderr"  \ -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl"  \ -p 8000:8000 \ -p 8443:8443 \ -p 8001:8001 \ -p 8444:8444 \ kong:latest


```

use kong:

```
curl -i http://localhost:8001/
```



### 安装kong-dashboard


```
docker run --rm -p 8080:8080 pgbi/kong-dashboard start --kong-url http://kong:8001
```


### 访问dashboard
[http://10.254.21.3:8080](http://10.254.21.3:8080)



### reference

[https://github.com/PGBI/kong-dashboard](https://github.com/PGBI/kong-dashboard)

[https://blog.csdn.net/jiangyu1013/article/details/80195583](https://blog.csdn.net/jiangyu1013/article/details/80195583)



