# Introduction

Dockerfile to build a ActiveMQ container image.

## Version

Current Version: **5.9.0**

# Hardware Requirements

## Memory

- **1GB** is the **standard** memory size. You should up that for production according to your needs.

## Storage

- Mostly, ActiveMQ stores things in memory, so no space is needed.  Should you start to persist to disk, consider attaching a data volume.

# How to Build a new Version

* Download JBoss A-MQ from http://www.jboss.org/products/amq/download/
* Put the file in the "install_files" directory
* Update the VERSION file
* run `batch.sh`

# Installation

Pull the image from the docker index. This is the recommended method of installation as it is easier to update image. These builds are performed by the **Docker Trusted Build** service.

```bash
docker pull jlgrock/activemq:5.9.0
```

Alternately you can build the image locally.

```bash
git clone https://github.com/jlgrock/docker.activemq.git
cd docker.activemq
docker build --tag="jlgrock/activemq" .
```