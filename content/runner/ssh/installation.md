---
date: 2000-01-01T00:00:00+00:00
title: Installation
author: bradrydzewski
weight: 2
toc: true
steps: true
description: |
  Install the runner using Docker.

aliases:
- /runners/ssh/install
---

This article explains how to install the ssh runner on Linux using Docker. The ssh runner is packaged as a minimal Docker image distributed on [DockerHub](https://hub.docker.com/r/drone/drone-runner-ssh).

# Download

Install Docker and pull the public image:

```
$ docker pull drone/drone-runner-ssh
```

# Configuration

The ssh runner is configured using environment variables. This article references the below configuration options. See [Configuration]({{< relref "configuration/reference" >}}) for a complete list of configuration options.

* __DRONE_RPC_HOST__
  : provides the hostname (and optional port) of your Drone server. The runner connects to the server at the host address to receive pipelines for execution.

* __DRONE_RPC_PROTO__
  : provides the protocol used to connect to your Drone server. The value must be either http or https.

* __DRONE_RPC_SECRET__
  : provides the shared secret used to authenticate with your Drone server. This must match the secret defined in your Drone server configuration.

# Installation

The below command creates the a container and start the ssh runner. _Remember to replace the environment variables below with your Drone server details._

```
$ docker run -d \
  -e DRONE_RPC_PROTO=https \
  -e DRONE_RPC_HOST=drone.company.com \
  -e DRONE_RPC_SECRET=super-duper-secret \
  -p 3000:3000 \
  --restart always \
  --name runner \
  drone/drone-runner-ssh
```

# Verification

Use the `docker logs` command to view the logs and verify the runner successfully established a connection with the Drone server.

```
$ docker logs runner

INFO[0000] starting the server
INFO[0000] successfully pinged the remote server 
```
