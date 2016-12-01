#Chạy Docker Engine, cAdvisor mỗi khi start VM

Sử dụng image: CoreOS

Mỗi khi chạy một VM mới, thêm đoạn script sau vào tham số user_data:

```
#!bin/bash

systemctl start docker.service

docker swarm init

docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  google/cadvisor:latest

  exit 0
```
