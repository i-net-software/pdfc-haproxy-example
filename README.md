# i-net PDFC Docker Example with HAProxy

This project is aimed at making it easier to start with a preconfigured [i-net PDFC](https://www.inetsoftware.de/products/pdf-content-comparer) server that can scale across nodes.

**Note:** This is not a manual on how to run a scaled PDFC setup in production!

## Quickstart

To get started quickly, clone the project and start the container ensemble with 5 i-net PDFC server instances:

	git clone https://github.com/i-net-software/pdfc-haproxy-example && cd pdfc-haproxy-example
	docker-compose up -d --build --scale pdfc=5

It will spin up the followng containers:

  * Five i-net PDFC server instances (can be scaled up or down; Check [inetsoftware/i-net-pdfc-server
](http://hub.docker.com/r/inetsoftware/i-net-pdfc-server) for details)
  * A [MongoDB](http://mongodb.com) server
  * An [HAProxy](http://www.haproxy.org) on port 80/443 with statistics module enabled
  * A DockerGen container translating the running docker containers into the HAProxy confguration

The containers will be started on the same host - so they are virtual instances not really scaling. But it should be quite easy to apply the configuration to a Swarm Cluster.

## Requirements

To start the given ensemble of containers it is required to have `docker` running and `docker-compose` available. Given the commands above it is very easy to start and scale i-net PDFC across a number of virtual nodes.

It is advisable to know how [HAProxy](http://www.haproxy.org) and [docker-gen](https://github.com/jwilder/docker-gen) work since the setup relies on them.

## Custom Configuration

The setup can be configured to a certain point. There is a `.env` file for the basic ensemble configuration.

By default the non-ssl version is run. If you have an SSL certificate you can configure it and use the SSL version. Please note the special format that a certificate (bundle) requires for HAProxy.

Further configration is available in the `docker-compose.yml`