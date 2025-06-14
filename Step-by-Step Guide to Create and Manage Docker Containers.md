## Step-by-Step Guide to Create and Manage Docker Containers

### 1. Create a Dockerfile

Start by defining your application environment in a `Dockerfile`:

```dockerfile
# Use an official base image
FROM node:lts-alpine

# Set working directory
WORKDIR /app

# Copy application files
COPY package.json ./
COPY src/ ./src

# Install dependencies
RUN yarn install --production

# Expose port and define startup command
EXPOSE 3000
CMD ["node", "src/index.js"]
```

This template uses Node.js but adapt for your stack (Python, Java, etc.) [^1][^5].

---

### 2. Build the Docker Image

```bash
docker build -t my-app:latest .
```

- `-t` tags the image (e.g., `my-app:latest`)
- `.` specifies the Dockerfile location [^1][^5][^8]

---

### 3. Run the Container

```bash
docker run -d -p 3000:3000 --name my-container my-app:latest
```

| Flag | Purpose |
| :-- | :-- |
| `-d` | Detached mode (run in background) |
| `-p` | Port mapping (host:container) |
| `--name` | Assign custom container name |

Verify running containers:

```bash
docker ps
```


---

### 4. Manage Container Lifecycle

#### Key States and Commands

| State | Command | Action |
| :-- | :-- | :-- |
| Created | `docker create` | Initialize without starting [^6] |
| Running | `docker start/run` | Start/restart container [^2][^7] |
| Paused | `docker pause/unpause` | Freeze/resume processes [^3][^4] |
| Stopped | `docker stop` | Graceful shutdown (SIGTERM) [^3][^7] |
| Deleted | `docker rm` | Remove permanently [^7] |

**Example workflow:**

```bash
docker stop my-container    # Gracefully stop
docker start my-container   # Restart
docker rm my-container      # Delete after stopping
```


---

### 5. Advanced Management

#### Persistent Storage

Mount volumes to retain data:

```bash
docker run -v /host/path:/container/path my-app
```

Create named volumes for easier management:

```bash
docker volume create app-data
docker run -v app-data:/app/data my-app
```


#### Resource Limits

Prevent resource hogging:

```bash
docker run --cpus 2 --memory 512m my-app
```

Monitor usage:

```bash
docker stats
```


---

### 6. Troubleshooting

| Task | Command |
| :-- | :-- |
| View logs | `docker logs my-container` |
| Inspect metadata | `docker inspect my-container` |
| Execute commands in container | `docker exec -it my-container sh` |

[^7][^8]

---

### Best Practices

1. **Use small base images** (e.g., `alpine` variants) to reduce size [^3]
2. **Implement health checks** in Dockerfile for reliability [^3]
3. **Automate cleanup** with `docker system prune` to remove unused resources [^3]
4. **Scan images** for vulnerabilities using `docker scan` [^3]

---

This workflow covers container creation, runtime management, and optimization strategies using core Docker CLI commands.

**⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References *⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂**

[^1]: https://docs.docker.com/get-started/workshop/02_our_app/

[^2]: https://learn.microsoft.com/en-us/dotnet/core/docker/build-container

[^3]: https://daily.dev/blog/docker-container-lifecycle-management-best-practices

[^4]: https://last9.io/blog/docker-container-lifecycle/

[^5]: https://www.datacamp.com/tutorial/docker-tutorial

[^6]: https://docs.docker.com/reference/cli/docker/container/create/

[^7]: https://www.hostinger.com/tutorials/docker-start-a-container

[^8]: https://www.incredibuild.com/blog/docker-101-a-comprehensive-tutorial-for-beginners

[^9]: https://dontpaniclabs.com/blog/post/2024/01/18/creating-and-running-a-docker-container-a-step-by-step-guide/

[^10]: https://labex.io/tutorials/docker-how-to-create-and-manage-docker-containers-quickly-392600

