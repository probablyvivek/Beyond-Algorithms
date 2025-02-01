### Introduction to Docker

Docker is a platform that allows you to develop, ship, and run applications in **containers**. Containers are lightweight, isolated environments that package an application and its dependencies, ensuring that it runs consistently across different environments.

### Why Docker?

Imagine you’re building an application that needs a specific version of Python, a database like MySQL, and a web server like Nginx. Without Docker, you’d have to manually install and configure all these components on your machine, and it might not work the same way on another machine. Docker solves this problem by packaging everything into a container, so it works the same way everywhere.

---

### Key Concepts

1. **Container**: A lightweight, standalone, and executable package that includes everything needed to run an application (code, runtime, libraries, etc.).
2. **Image**: A template or blueprint for creating containers. It’s like a snapshot of a container.
3. **Dockerfile**: A text file that contains instructions for building a Docker image.
4. **Docker Hub**: A public registry where you can find and share Docker images.

---

### Getting Started with Docker

#### 1. **Check Docker Installation**
First, let’s make sure Docker is installed and running. Open your terminal and run:

```bash
docker --version
```

This should display the Docker version installed on your system.

#### 2. **Run Your First Container**
Let’s run a simple container using the `hello-world` image:

```bash
docker run hello-world
```

**What’s happening here?**
- Docker looks for the `hello-world` image on your local machine.
- If it doesn’t find it, it downloads it from Docker Hub.
- Then, it runs the container, which prints a "Hello from Docker!" message.

#### 3. **Run a Web Server (Nginx)**
Let’s run a more practical example: a web server using the `nginx` image.

```bash
docker run -d -p 8080:80 nginx
```

**What’s happening here?**
- `docker run`: Runs a container.
- `-d`: Runs the container in the background (detached mode).
- `-p 8080:80`: Maps port 8080 on your machine to port 80 in the container (Nginx runs on port 80 by default).
- `nginx`: The image to use.

Now, open your browser and go to `http://localhost:8080`. You should see the Nginx welcome page.

#### 4. **List Running Containers**
To see all running containers, use:

```bash
docker ps
```

This will show you the container ID, image name, status, and ports.

#### 5. **Stop a Container**
To stop the Nginx container, first get the container ID using `docker ps`, then run:

```bash
docker stop <container_id>
```

Replace `<container_id>` with the actual ID of your container.

#### 6. **Remove a Container**
Once stopped, you can remove the container:

```bash
docker rm <container_id>
```

#### 7. **List Docker Images**
To see all the images you’ve downloaded:

```bash
docker images
```

#### 8. **Remove an Image**
If you want to remove an image, use:

```bash
docker rmi <image_name>
```

---

### Building Your Own Docker Image

Let’s create a simple Docker image for a Python application.

#### 1. **Create a Dockerfile**
Create a file named `Dockerfile` (no file extension) in your project directory with the following content:

```Dockerfile
# Use an official Python image as the base
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port 5000 for the application
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

#### 2. **Create a Simple Python App**
Create a file named `app.py` in the same directory:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

#### 3. **Create a `requirements.txt` File**
Create a file named `requirements.txt` with the following content:

```
Flask==2.0.1
```

#### 4. **Build the Docker Image**
Run the following command to build the Docker image:

```bash
docker build -t my-python-app .
```

- `-t my-python-app`: Tags the image with the name `my-python-app`.
- `.`: Specifies the current directory as the build context.

#### 5. **Run the Container**
Now, run the container:

```bash
docker run -d -p 5000:5000 my-python-app
```

Visit `http://localhost:5000` in your browser, and you should see "Hello, Docker!".

---

### Common Docker Commands

| Command                          | Description                                      |
|----------------------------------|--------------------------------------------------|
| `docker run <image>`             | Run a container from an image.                  |
| `docker ps`                      | List running containers.                        |
| `docker ps -a`                   | List all containers (running and stopped).      |
| `docker stop <container_id>`     | Stop a running container.                       |
| `docker rm <container_id>`       | Remove a stopped container.                     |
| `docker images`                  | List all images.                                |
| `docker rmi <image_name>`        | Remove an image.                                |
| `docker build -t <name> .`       | Build an image from a Dockerfile.               |
| `docker logs <container_id>`     | View logs of a container.                       |
| `docker exec -it <container_id> /bin/bash` | Open a shell inside a running container. |

---

### Why Use Docker?

1. **Consistency**: Your application runs the same way in development, testing, and production.
2. **Isolation**: Each container is isolated, so you can run multiple applications without conflicts.
3. **Portability**: You can easily move containers between different environments.
4. **Efficiency**: Containers share the host OS kernel, making them lightweight and fast.

---

### Next Steps

1. **Explore Docker Hub**: Visit [Docker Hub](https://hub.docker.com/) to find pre-built images for popular software like MySQL, Redis, and more.
2. **Learn Docker Compose**: Docker Compose allows you to define and run multi-container applications.
3. **Dive Deeper**: Learn about Docker networking, volumes, and advanced topics like Docker Swarm and Kubernetes.

---

### Final Words

Docker is a powerful tool that simplifies application development and deployment. By following the steps above, you’ve already taken your first steps into the world of containers. Keep experimenting, and soon you’ll be able to containerize any application! 🚀
