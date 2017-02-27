# wordpress-swarm

This *example project* will create 2 services in a Docker swarm mode cluster:
* Two Wordpress containers listening on port 8080
* One MariaDB database configured for Galera-based clustering using swarm mode DNS for discovery

Note this is for demonstration purposes, only. To run clustered
wordpress, one will need to address session state across wordpress
containers, and improved storage for the MariaDB containers.

# Usage

These services can be started using the following command:
    
```
docker stack deploy --compose-file docker-stack.yml wordpress
```

This will bring up 2 wordpress containers, and a single dbcluster
container. To see an example of scaling up MariaDB to 3 nodes
(generally for databases you want an odd number of nodes), try:

```
docker service scale wordpress_dbcluster=3
```

When finished, the following command shuts everything down:

```
docker service rm dbcluster wordpress
```

# References
This project uses the following Docker images:
* PHP 7.1/Apache version of the [Official Docker Wordpress image](https://hub.docker.com/_/wordpress/)
* ToughIQ's [MariaDB Galera Cluster image](https://hub.docker.com/r/toughiq/mariadb-cluster/)
