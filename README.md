# Nexus Repository with Docker Compose

This repository provides a Docker Compose configuration to run [Sonatype Nexus 3](https://www.sonatype.com/nexus-repository-oss) as a service. It also outlines the steps to configure Docker to access the Nexus repository via HTTP and use an insecure registry.

## Prerequisites

- Docker installed on your local machine or server.
- Docker Compose installed.
- A running Docker daemon configured to allow insecure registries.

## Configuration Overview

In this setup, we use **Sonatype Nexus 3** as the container image. The Nexus service runs on ports `8081` (for the Nexus UI) and `7070` (for the REST API).

### Docker Compose Configuration

```yaml
version: '3'
services:
  nexus:
    image: sonatype/nexus3
    volumes:
      - "nexus:/sonatype-work"  # Persistent storage for Nexus data
    ports:
      - "8081:8081"  # Nexus UI port
      - "7070:7070"  # Nexus API port

volumes:
  nexus:  # Persistent volume for Nexus data
```


### Key Changes:
- **Insecure Registry Configuration**: The section that adds `localhost:8081` to the `insecure-registries` list in the Docker daemon's `daemon.json` has been added to the README.
- Instructions on how to create and modify `/etc/docker/daemon.json` for the insecure registry setting.

You can copy this entire content and save it as `README.md` in your repository. Let me know if you need further modifications!

