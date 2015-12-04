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
_________________________________________________________________

####How Observer works

The config server listens incoming HTTP traffic and allows to add or remove CoAP devices (clients).

It provides the next entry points:

```
- /clients (retrieves the list of all devices)

- /clients/add (adds a new device and invokes Register event to register observable resources), this is a POST request whith next data format
    {"host": "IP address", "port": "PORT"}
    
- /clients/delete/:id (removes the device from the config and then invoke Deregister event)
    where id - the unique identifier of device
```

The observer listens UDP traffic and processes Json data only then sends the processed data to the ElasticSearch.

If incoming JSON data include the "type" field that its value will be used as a type for ElasticSearch. In other case will be used default type - "type".