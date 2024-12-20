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



###  Set Docker Daemon to Use Insecure Registry

In order to push and pull Docker images to/from the Nexus repository using HTTP (insecure registry), you need to configure your Docker daemon to allow insecure registries.

#### Steps:

1. Edit the Docker daemon configuration file (`/etc/docker/daemon.json`) on your local machine or server.

    If the file does not exist, create it.

    ```bash
    sudo nano /etc/docker/daemon.json
    ```

2. Add the following content to the file:

    ```json
    {
      "insecure-registries": ["localhost:8081"]
    }
    ```

    This tells Docker that your Nexus registry (running on `localhost` port `8081`) is an insecure registry, which allows Docker to push and pull images over HTTP.

3. Restart the Docker daemon to apply the changes:

    ```bash
    sudo systemctl restart docker
    ```

This configuration will allow Docker to interact with the Nexus registry over HTTP.


