## Redis with Docker

Create redis container
```
$docker image pull redis:5.0.5
$docker container run -d -p 6379:6379 --name redis1 redis:5.0.5
$docker container ps
$docker container logs redis1
```

Run with redis-cli
```
$docker container exec -it redis1 sh
#redis-cli
>ping

PONG
```

Basic command with redis
```
>set name somkiat
>get name
>incr counter
>incr counter
>get counter
```

Redis performacne testing
```
#redis-benchmark -t get -n 10000
```

Redis monitoring command
```
>MONITORING
>INFO
>INFO clients
>INFO stats
```

Redis monitoring with Prometheus
```
```


More for [Redis command](https://redis.io/commands)