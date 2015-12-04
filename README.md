# Observer

Observing Resources in the Constrained Application Protocol

##Installation

1. Install [Docker](https://www.docker.com)

2. Download automated build from public Docker Hub Registry: `docker pull qapps/coap-service`
(alternatively, you can build an image from Dockerfile: `docker build -t="qapps/coap-service" github.com/qualiapps/coap-service`)

###Start Observer

`docker run -d -p 4000:4000 -p 56083:56083 --name observer qapps/coap-service [options]`


####Specify these options, if you want to change some params

####options:
```
-conf - config file (default: clients.db)

-port - config server port (default: 4000)

-lport - port to listen incoming CoAP traffic (resource notification)
```

#### Available environment vars

```
ES_HOST - elasticsearch host (default: localhost)

ES_PORT - elasticsearch port (default: 9200)

ES_INDEX - index name (default: index)
```