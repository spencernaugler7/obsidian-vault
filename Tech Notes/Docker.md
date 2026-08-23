```bash
# List all running Docker containers
docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Names}}\t{{.Status}}"

# List all containers including stopped ones
docker ps -a --format "table {{.ID}}\t{{.Image}}\t{{.Names}}\t{{.Status}}"

# List all Docker images
docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}"

# List Docker volumes
docker volume ls

# List Docker networks
docker network ls

# Export the full list for reference
docker ps -a --format json > /tmp/docker-containers.json
docker images --format json > /tmp/docker-images.json
```
