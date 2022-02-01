### Handmade CDN

### Setup

1. Install docker

## Steps to run

1. `docker network create --gateway 172.16.1.1 --subnet 172.16.1.0/24 task13_subnet`
2. `docker-compose up --build` 
   

### Results


# Testing CDN
```
docker exec -it hlsa_task13_tester_1 ping cdn.super.hot

PING cdn.super.hot (172.16.1.30) 56(84) bytes of data.
64 bytes from hlsa_task13_load_balancer_world_1.task13_subnet (172.16.1.30): icmp_seq=1 ttl=64 time=0.069 ms
```


# Testing Load Balancers
```
docker-compose run --rm siege -c25 -t10s -b "http://cdn.super.hot/bmw.png"
```

- **Cache on**
```
Transactions:                 117590 hits
Availability:                 100.00 %
Elapsed time:                   9.69 secs
Data transferred:           10291.05 MB
Response time:                  0.00 secs
Transaction rate:           12135.19 trans/sec
Throughput:                  1062.03 MB/sec
Concurrency:                   24.64
Successful transactions:      117592
Failed transactions:               0
Longest transaction:            0.50
Shortest transaction:         
```

- **Cache off**
- **Round Robin**
```
Transactions:                  59166 hits
Availability:                 100.00 %
Elapsed time:                   9.80 secs
Data transferred:            5177.91 MB
Response time:                  0.00 secs
Transaction rate:            6037.35 trans/sec
Throughput:                   528.36 MB/sec
Concurrency:                   24.81
Successful transactions:       59166
Failed transactions:               0
Longest transaction:            0.73
Shortest transaction:           0.00
```

- **Cache off**
- **least_conn**
```
Transactions:                  57555 hits
Availability:                 100.00 %
Elapsed time:                   9.01 secs
Data transferred:            5036.92 MB
Response time:                  0.00 secs
Transaction rate:            6387.90 trans/sec
Throughput:                   559.04 MB/sec
Concurrency:                   24.80
Successful transactions:       57555
Failed transactions:               0
Longest transaction:            0.79
Shortest transaction:           0.00
```
