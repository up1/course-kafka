## Redis with Docker

Create redis container
```
$docker image pull redis:5.0.5
$docker container run -d -p 6379:6379 --name redis1 redis:5.0.5
$docker container run -d -p 6379:6379 --name redis1 redis:5.0.5 --maxmemory 1gb
$docker container ps
$docker container logs redis1
```

### Run with redis-cli
```
$docker container exec -it redis1 sh
#redis-cli
>ping

PONG
```

### Basic command with redis
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

### Redis monitoring command
```
>MONITORING
>INFO
>INFO clients
>INFO stats
```

More for [Redis command](https://redis.io/commands)

### Redis monitoring with Prometheus
Download files
* [Redis exporter](https://github.com/oliver006/redis_exporter/releases)
* [Redis dashboard for Prometheus](https://grafana.com/grafana/dashboards/763)

Run redis exporter
```
$redis_exporter -redis.addr redis://localhost:6379
```
Open url=http://localhost:9121/metrics in browser

Edit file prometheus.yml
```
scrape_configs:
  - job_name: 'redis-server' 
    static_configs: 
    - targets: ['127.0.0.1:9121']
```

### Reference Websites
* [Redis on windows](https://redislabs.com/blog/redis-on-windows-8-1-and-previous-versions/)
