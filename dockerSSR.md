yum install epel-release -y
yum install docker-io -y
systemctl start docker
docker pull hub.c.163.com/alechy/dockerssr
docker ps -a
docker images
docker create --name "DockerSSR" -i -t --cap-add NET_ADMIN --cap-add NET_RAW -p 0.0.0.0:80:80/tcp -p 0.0.0.0:80:80/udp -p 0.0.0.0:8080:8080/tcp -p 0.0.0.0:8080:8080/udp -p 0.0.0.0:137:137/tcp -p 0.0.0.0:137:137/udp -p 0.0.0.0:138:138/tcp -p 0.0.0.0:138:138/udp -p 0.0.0.0:53:53/tcp -p 0.0.0.0:53:53/udp hub.c.163.com/alechy/dockerssr
docker ps -a
docker logs CONTAIN_ID
docker exec -it CONTAIN_ID /bin/bash
