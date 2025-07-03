# Docker安装RocketMQ 5.3.4
dockcer-compose.yml

```plain
version: '3.8'
services:
  namesrv:
    image: apache/rocketmq:5.3.1
    container_name: rmqnamesrv
    ports:
      - 9876:9876
    networks:
      - rocketmq
    command: sh mqnamesrv

  broker:
    image: apache/rocketmq:5.3.1
    container_name: rmqbroker
    ports:
      - 10909:10909
      - 10911:10911
      - 10912:10912
    volumes:
      - ./broker.conf:/home/rocketmq/rocketmq-5.3.1/conf/broker.conf
    environment:
      - NAMESRV_ADDR=rmqnamesrv:9876
    depends_on:
      - namesrv
    networks:
      - rocketmq
    command: sh mqbroker -n rmqnamesrv:9876 -c /home/rocketmq/rocketmq-5.3.1/conf/broker.conf

  dashboard:
    image: apacherocketmq/rocketmq-dashboard:latest
    container_name: rmq-dashboard
    ports:
      - 8082:8080
    networks:
      - rocketmq
    depends_on:
      - namesrv
    environment:
      - JAVA_OPTS=-Drocketmq.config.namesrvAddr=rmqnamesrv:9876
    restart: unless-stopped

networks:
  rocketmq:
    driver: bridge
```

同级目录下`broker.conf`文件

```plain
brokerClusterName = DefaultCluster
brokerName = broker-a
brokerId = 0
deleteWhen = 04
fileReservedTime = 48
brokerRole = ASYNC_MASTER
flushDiskType = ASYNC_FLUSH
# 下面这个ip是宿主机的内网ip
brokerIP1 =  192.168.92.177
```

