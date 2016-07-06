# Introduction

Dockerfile to build a JBoss ActiveMQ container image.  This sits upon Apache Karaf, has integrated Apache Qpid (for AMQP) and Apache Camel inside the Message Broker (for flexible messaging), and thus gives multi-protocol, multi-language support (out of the box.

A-MQ is embeddable and highly available.  Currently this image acts as a stand-alone container in single-node availability.

# Hardware Requirements

## Memory

- **1GB** is the **standard** memory size. You should up that for production according to your needs.

## Storage

- Mostly, ActiveMQ stores things in memory, so no space is needed.  Should you start to persist to disk, consider attaching a data volume.

# How to get the image

You can either download the image from a docker registry or build it yourself.

## Building a new Version

* Download JBoss A-MQ from http://www.jboss.org/products/amq/download/
* Put the file in the "install_files" directory
* Update the VERSION file
* run `build.sh`

## Downloading from a Docker Registry

These builds are not performed by the **Docker Trusted Build** service because it contains JBoss proprietary code, but this method can be used if using a [Private Docker Registry](https://docs.docker.com/registry/deploying/).

```bash
docker pull jlgrock/jboss-amq:$VERSION
```

## SSL Configuration Parameters

Below is a complete list of available options that can be used to start JBoss AMQ with SSL.

- **--ssl**: Starts JBoss AMQ with SSL
- **--ssl-host**: Sets the SSL URL/IP, e.g., `--ssl-host 0.0.0.0`
- **--ssl-port**: Sets SSL port, e.g., `--ssl-port 61616`

When starting JBoss AMQ with SSL the following files must be present:
- **/amq/store/broker/broker.ks**: Broker KeyStore file
- **/amq/store/broker/broker.ts**: Broker TrustStore file
- **/amq/store/pw/keystore_pw**: KeyStore password file containing the broker.ks and broker.ts password encrypted using [Jasypt](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_A-MQ/6.2/html/Security_Guide/FMQSecurityEncryptProperties.html)

# Examples of Running a Container

The following will map all exposed ports
```bash
docker run -it --rm -p 8101:8101 -p 8181:8181 -p 44444:44444 -p 1099:1099 -p 61616:61616 jlgrock/jboss-amq:6.2.0
```

The following will start JBoss AMQ with SSL
```bash
docker run -it --rm -p 8101:8101 -p 8181:8181 -p 44444:44444 -p 1099:1099 -p 61616:61616 jlgrock/jboss-amq:6.2.0 --ssl --ssl-host 0.0.0.0 --ssl-port 61616
```
