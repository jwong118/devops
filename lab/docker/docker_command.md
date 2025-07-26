# Common Docker commands

# Build an image from a Dockerfile
docker build -t <image_name> .

# List all Docker images
docker images

# Run a container from an image
docker run -d --name <container_name> <image_name>

# Run a container from an image in interactive mode
docker run -d --name myubuntu -i ubuntu

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop a running container
docker stop <container_name>

# Remove a container
docker rm <container_name>

# Remove an image
docker rmi <image_name>

# View logs from a container
docker logs <container_name>

# Execute a command inside a running container
docker exec -it <container_name> /bin/bash
docker exec myubuntu whomai
docker exec myubuntu cat /etc/lsb-release

# Show the running process
docker top <container_name>

Dockerfile Example
cat > Dockerfile <<EOL
FROM ubuntu:20.04

RUN apt update && apt install nginx -y

ENTRYPOINT ["/bin/bash", "-c"]

CMD ["service nginx start"]
EOL

#Re-build the image and run the image with the following command
docker build -t custom-nginx .
docker rm -f custom-nginx-container
docker run -d -it --name custom-nginx-container custom-nginx
docker ps

#Run the same image using a different name (remember --name option?) with a bash towards the end.
docker run -d --name nginx-one -it custom-nginx bash
docker ps