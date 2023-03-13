# README

This is a placeholder project. It provides a running and available docker swarm network which will be used subsequently by
other services and especially by the gateway itself to expose endpoints to the web. It only needs to be startet once.
Separating it means to prevent deletion on teardown of other services or conflicts with other services.

If you want to expose an service for the RGDZ stack your service should be bound to the netowork named:

```
rgdz_gateway_network_public
```

Through defining a subnet space we also ensure to pin settings and prevent orphan service discovery randomly by restarting
services. Better be explicit than sorry.

To start the meta stack:

```shell
docker stack deploy rgdz_gateway_network -c rgdz.gateway.network/docker-compose.yml
```

To check if everything went well:

```shell
docker service ls
```

should show

```
ID             NAME                           MODE         REPLICAS   IMAGE            PORTS
XXXXXXXXXXXX   rgdz_gateway_network_scratch   replicated   0/0        scratch:latest
```

which means the network is created an will be there to serve our services.
