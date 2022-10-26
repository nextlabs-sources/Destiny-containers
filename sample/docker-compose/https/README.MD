## Docker Compose file for the whole set up

### Steps

To start the containers from scratch:

First, modify .env file to suit your needs.

```shell
docker-compose up dbinit certificate_generator
docker-compose up -d dms dps dac dabs cas reporter administrator console
# wait a while for containers to start and start the nginx proxy
docker-compose up -d proxy
```

To shudown and remove the containers and certificates and networks:

```shell
docker-compose down -v
```