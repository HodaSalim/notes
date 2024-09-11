# Comprehensive Docker Guide for BuildStream

## 1. Introduction to Docker

Docker is a platform for developing, shipping, and running applications in containers. Containers are lightweight, standalone, executable packages that include everything needed to run a piece of software, including the code, runtime, system tools, libraries, and settings.

Key benefits of using Docker:
- Consistency across development, testing, and production environments
- Isolation of applications and their dependencies
- Efficient resource utilization
- Easy scaling and deployment of services

## 2. Installing Docker

### 2.1 For Windows:
1. Download Docker Desktop for Windows from the official Docker website.
2. Run the installer and follow the prompts.
3. Once installed, start Docker Desktop.

### 2.2 For macOS:
1. Download Docker Desktop for Mac from the official Docker website.
2. Open the .dmg file and drag the Docker icon to your Applications folder.
3. Open Docker from your Applications folder.

### 2.3 For Linux (Ubuntu):
1. Update your package index:
   ```
   sudo apt-get update
   ```
2. Install packages to allow apt to use a repository over HTTPS:
   ```
   sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
   ```
3. Add Docker's official GPG key:
   ```
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```
4. Set up the stable repository:
   ```
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```
5. Update the package index again:
   ```
   sudo apt-get update
   ```
6. Install Docker:
   ```
   sudo apt-get install docker-ce
   ```

## 3. Docker Basics

### 3.1 Key Docker Concepts
- **Image**: A lightweight, standalone, executable package that includes everything needed to run a piece of software.
- **Container**: A runtime instance of an image.
- **Dockerfile**: A text file that contains instructions for building a Docker image.
- **Docker Compose**: A tool for defining and running multi-container Docker applications.

### 3.2 Basic Docker Commands
- `docker pull <image>`: Download an image from Docker Hub
- `docker run <image>`: Create and start a container from an image
- `docker ps`: List running containers
- `docker ps -a`: List all containers (including stopped ones)
- `docker stop <container>`: Stop a running container
- `docker rm <container>`: Remove a container
- `docker images`: List downloaded images
- `docker rmi <image>`: Remove an image

## 4. Dockerizing BuildStream Services

### 4.1 Creating a Dockerfile
For each microservice in BuildStream, create a Dockerfile. Here's an example for the User Service:

```Dockerfile
# Use the official Golang image as a parent image
FROM golang:1.17

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files
COPY go.mod go.sum ./

# Download the dependencies
RUN go mod download

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o main .

# Expose port 8080 to the outside world
EXPOSE 8080

# Command to run the executable
CMD ["./main"]
```

Save this as `Dockerfile` in the root directory of your User Service.

### 4.2 Building the Docker Image
Navigate to the directory containing the Dockerfile and run:

```
docker build -t buildstream-user-service .
```

This command builds a Docker image named `buildstream-user-service` based on the instructions in the Dockerfile.

### 4.3 Running the Container
To run the container:

```
docker run -p 8080:8080 buildstream-user-service
```

This command starts a container from the `buildstream-user-service` image and maps port 8080 in the container to port 8080 on your host machine.

## 5. Using Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It's perfect for orchestrating all the services in BuildStream.

### 5.1 Creating a docker-compose.yml File
Create a file named `docker-compose.yml` in the root of your project:

```yaml
version: '3'
services:
  user-service:
    build: ./user-service
    ports:
      - "8080:8080"
    depends_on:
      - mysql

  studio-service:
    build: ./studio-service
    ports:
      - "8081:8081"
    depends_on:
      - mysql
      - elasticsearch

  streaming-service:
    build: ./streaming-service
    ports:
      - "8082:8082"
    depends_on:
      - rabbitmq

  chat-service:
    build: ./chat-service
    ports:
      - "8083:8083"
    depends_on:
      - rabbitmq
      - redis

  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: buildstream
    volumes:
      - mysql-data:/var/lib/mysql

  redis:
    image: redis:6

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.15.0
    environment:
      - discovery.type=single-node

  rabbitmq:
    image: rabbitmq:3-management

volumes:
  mysql-data:
```

This `docker-compose.yml` file defines all the services for BuildStream, including the microservices and their dependencies.

### 5.2 Running the Application with Docker Compose
To start all services defined in `docker-compose.yml`:

```
docker-compose up
```

To run it in detached mode (in the background):

```
docker-compose up -d
```

To stop all services:

```
docker-compose down
```

## 6. Best Practices for Docker in BuildStream

1. **Use specific tags for base images**: Instead of using `latest`, specify a version, e.g., `golang:1.17`.

2. **Optimize Dockerfile for caching**: Put commands that are less likely to change (like installing dependencies) before commands that are more likely to change (like copying source code).

3. **Use multi-stage builds**: For smaller final images, especially for Go applications.

4. **Don't run containers as root**: Use the `USER` instruction in your Dockerfile to switch to a non-root user.

5. **Use environment variables**: For configuration that might change between environments.

6. **Implement health checks**: Use the `HEALTHCHECK` instruction in your Dockerfile to tell Docker how to test that your app is still working.

7. **Use Docker secrets for sensitive data**: Instead of hardcoding passwords or API keys.

## 7. Debugging Docker Containers

- To see logs from a container: `docker logs <container_id>`
- To enter a running container: `docker exec -it <container_id> /bin/bash`
- To inspect a container: `docker inspect <container_id>`

## 8. Deploying Docker Containers

For production deployment, consider using orchestration tools like Kubernetes or Docker Swarm. These tools help manage scaling, load balancing, and rolling updates of your containerized applications.

Remember, mastering Docker takes time and practice. Start with containerizing one service, then gradually move to containerizing all services and using Docker Compose to orchestrate them.
