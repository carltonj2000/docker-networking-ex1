# Docker Networking

```bash
docker run --rm -d --name nginx -p 80:80 nginx
docker inspect nginx
ip a | grep docker0
docker network ls
docker network create custombridge
docker network ls
ip a | grep 6d21
docker run --name netshoot --rm -it --network custombridge nicolaka/netshoot /bin/bash
> ip a
> ping 172.17.0.2 # fails pinging nginx server on other bridge/network
docker run --name netshoot2 --rm -it --network custombridge nicolaka/netshoot /bin/bash
> ping netshoot
docker stop nginx
docker run --rm -d --name nginx --network host nginx
docker ps | grep nginx
docker inspect nginx
ss -ltup
docker run --rm -d --name nginx2 --network host nginx # fails due to port conflict
docker network create -d macvlan --subnet 192.168.50.0/24 --gateway 192.168.50.1 --ip-range 192.168.50.77/32 -o parent=enp12s0 custommacvlan # unused by gateway
docker network ls
docker run --name netshoot --rm -it --network custommacvlan nicolaka/netshoot /bin/bash
docker run --name netshoot2 --rm -it --network custommacvlan --ip 192.168.50.78 nicolaka/netshoot /bin/bash
> ping netshoot
> ping netshoot2
> ping renderws.home
> ping mediapc.home
```

## Repo History

The notes in this repository are based on the following:

- [Docker Networking Tutorial](https://youtu.be/5grbXvV_DSk)
