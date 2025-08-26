# velociraptor-docker
Run [Velocidex Velociraptor](https://github.com/Velocidex/velociraptor) server with Docker

## Current Version
This Docker setup is configured to use **Velociraptor v0.74.5** (latest stable release as of August 2025).

## Acknowledgment
This repository is based on [weslambert/velociraptor-docker](https://github.com/weslambert/velociraptor-docker).

## Installation

- Ensure [docker-compose](https://docs.docker.com/compose/install/) is installed on the host
- `git clone https://github.com/graype28/velociraptor-docker`
- `cd velociraptor-docker`
- Copy the example environment file: `cp .env.example .env`
- Edit `.env` and change the default credentials and configuration as desired
- `docker-compose up` (or `docker-compose up -d` for detached)
- Access the Velociraptor GUI via https://\<hostip\>:8889 
  - Default u/p is `admin/password` (or whatever you set in `.env`)
  - This can be changed by running: 
  
  `docker exec -it velociraptor ./velociraptor --config server.config.yaml user add user1 user1 --role administrator`

## Features

- **Latest Velociraptor v0.74.5** with all recent security updates and features
- **Multi-platform client support**: Automatically downloads and packages Linux, macOS, and Windows client binaries
- **Auto-repacking**: Client binaries are automatically repacked with server configuration
- **Certificate management**: Automatic SSL certificate rotation
- **Modern Docker Compose**: Uses compose file version 3.8 for better compatibility

## Notes

- Linux, Mac, and Windows binaries are located in `/velociraptor/clients`, which is mapped to the host in the `./velociraptor` directory
- Client binaries are automatically repacked based on the server configuration
- Once started, edit `server.config.yaml` in `/velociraptor`, then run `docker-compose down/up` for the server to reflect changes
- The container includes all 421+ built-in Velociraptor artifacts
- Supports all Velociraptor 0.74.5 features including Sigma rule support, enhanced ETW monitoring, and more

## Ports

- `8000`: Frontend (client communication)
- `8001`: API server (gRPC)
- `8889`: Web GUI

## Environment Variables

Set these in your `.env` file:

- `VELOX_USER`: Admin username (default: admin)
- `VELOX_PASSWORD`: Admin password (default: admin)
- `VELOX_ROLE`: User role (default: administrator)
- `VELOX_SERVER_URL`: Server URL for clients (default: https://localhost:8000/)
- `VELOX_FRONTEND_HOSTNAME`: Frontend hostname (default: localhost)

## Docker Hub Image

The Docker image is available on Docker Hub:

### Pull the latest version:
```bash
docker pull graype28/velociraptor:latest
```

### Pull a specific version:
```bash
docker pull graype28/velociraptor:0.74.5
```

### Use in docker-compose.yaml:
Instead of building locally, you can use the pre-built image by uncommenting and modifying the image line:
```yaml
services:
  velociraptor:
    image: graype28/velociraptor:0.74.5
    # build:
    #   context: ./
    #   dockerfile: Dockerfile
```

## Recent Updates (August 2025)

- Updated to Velociraptor v0.74.5 (from v0.74.2)
- Fixed download URLs for latest release format
- Updated Docker Compose to version 3.8
- Published Docker image to Docker Hub
- Verified compatibility with latest Velociraptor features
