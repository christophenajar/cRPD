
# Juniper Containerized RPD (cRPD) 

Containerized routing protocol process (cRPD) is Juniper’s routing protocol process (rpd) decoupled from Junos OS and packaged as a Docker container to run in Linux-based environments.

# Supported Features on cRPD
- BGP Route Reflector in the Linux container
- BGP add-path, multipath, graceful restart helper mode
- BGP, OSPF, OSPFv3, IS-IS, and Static
- BMP, BFD, and Linux-FIB
- Equal-Cost Multipath (ECMP)
- JET for Programmable RPD
- Junos CLI support
- Management using open interfaces NETCONF, and SSH
- Support for IPv4 and IPv6 routing


# Requirement

### Resources
 - RAM 256 MB
 - CPU 1 Core
 - Disk Space 256 MB

### Tools
 - Docker Engine 18.09.1


# Download the cRPD Software

The cRPD software is available as a cRPD Docker file from the Juniper Internal Docker registry.

There are two ways to download the software:

- Juniper software download page
- Juniper Docker Registry

# Configuration with Docker 

Load cRPD docker file 

```
$ docker load -i junos-routing-crpd-docker-19.4R1.10.tgz
```

Check cRPD image 

```
$ docker image ls
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
crpd                           19.4R1.10           5b6acdd96efb        2 months ago        320MB
```

Create data volume for configuration and var logs

```
$ docker volume create crpd01-config

$ docker volume create crpd01-varlog
```

Attach the data volumes to create and launch the container to the cRPD instance

```
$ docker run --rm --detach --name crpd01 -h crpd01 --net=bridge --privileged -v crpd01-config:/config -v crpd01-varlog:/var/log -m 512MB --memory-swap=512MB  -it crpd:19.4R1.10
```

Log in to the cRPD container

```
$ docker exec -it crpd01 cli
root@crpd01>
```

To view container processes

```
docker exec crpd01 ps aux
```

Stop the existing container

```
$ docker stop crpd01
```


# More details

https://www.juniper.net/documentation/en_US/crpd/topics/concept/understanding-crpd.html


