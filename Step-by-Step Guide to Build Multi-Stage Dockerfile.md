
## Step-by-Step Guide to Build Multi-Stage Dockerfiles

### 1. **Understand Multi-Stage Builds**

Multi-stage Docker builds separate the build environment (tools, dependencies) from the runtime environment. This reduces final image size and removes unnecessary build tools from production.

---

### 2. **Create a Basic Multi-Stage Dockerfile**

Example for a Go application:

```dockerfile  
# Stage 1: Build the application  
FROM golang:1.22 AS builder  
WORKDIR /app  
COPY . .  
RUN go build -o /bin/myapp  

# Stage 2: Runtime image  
FROM alpine:3.20  
COPY --from=builder /bin/myapp /bin/myapp  
CMD ["/bin/myapp"]  
```

- **Stage 1** (`builder`): Uses a Go image to compile the binary.
- **Stage 2**: Copies only the compiled binary into a lightweight Alpine image.

---

### 3. **Optimize Dependency Management**

For Node.js applications:

```dockerfile  
# Stage 1: Install dependencies (cached unless package.json changes)  
FROM node:22-slim AS deps  
WORKDIR /app  
COPY package*.json ./  
RUN npm ci  

# Stage 2: Build  
FROM node:22-slim AS build  
WORKDIR /app  
COPY --from=deps /app/node_modules ./node_modules  
COPY . .  
RUN npm run build  

# Stage 3: Runtime  
FROM nginx:alpine  
COPY --from=build /app/dist /usr/share/nginx/html  
```

- Use `.dockerignore` to exclude `node_modules` and other unnecessary files.

---

### 4. **Build Specific Stages**

Use `--target` to build individual stages (e.g., for testing):

```bash  
docker build --target deps -t myapp-deps .  
```


---

### 5. **Leverage BuildKit for Parallelism**

Enable BuildKit for faster builds and better caching:

```bash  
DOCKER_BUILDKIT=1 docker build -t myapp .  
```


---

### 6. **Verify Image Size Reduction**

Compare image sizes before/after multi-stage builds:

```bash  
docker images  
```

Example output:

```  
REPOSITORY   TAG       IMAGE ID       SIZE  
myapp        latest    8d2d8e7a1c2d   12MB  # Final alpine-based image  
builder      latest    a1b2c3d4e5f6   1.2GB # Intermediate build image  
```


---

### 7. **Advanced Use Cases**

#### **Reuse Common Stages**

```dockerfile  
# Shared base stage  
FROM python:3.11-slim AS base  
WORKDIR /app  

# Development stage (with debug tools)  
FROM base AS dev  
RUN apt-get update && apt-get install -y curl  
CMD ["python", "app.py"]  

# Production stage  
FROM base AS prod  
COPY requirements.txt .  
RUN pip install --no-cache-dir -r requirements.txt  
COPY . .  
CMD ["gunicorn", "app:app"]  
```


#### **Test in Intermediate Stages**

```dockerfile  
FROM node:22 AS test  
COPY --from=deps /app/node_modules ./node_modules  
COPY . .  
RUN npm test  
```


---

### Best Practices

1. **Minimize Layers**
Combine related commands (e.g., `RUN apt-get update && apt-get install -y curl`).
2. **Use Lightweight Base Images**
Prefer `alpine`, `distroless`, or `scratch` for final stages.
3. **Leverage Caching**
Order Dockerfile instructions from least to most frequently changed.
4. **Clean Up**
Remove temporary files in the same `RUN` layer:

```dockerfile  
RUN npm install && npm cache clean --force  
```

5. **Use `.dockerignore`**
Exclude build artifacts, logs, and local configs:

```  
node_modules  
.git  
Dockerfile  
```


---

### Example Workflow

1. Build and tag:

```bash  
docker build -t myapp:latest .  
```

2. Run:

```bash  
docker run -d -p 3000:80 myapp:latest  
```


---

This approach reduces image sizes by **~90%** in many cases (e.g., from 1.2GB to 120MB) while improving security by excluding build tools from production.

### References

- https://docs.docker.com/build/building/multi-stage/
- https://docs.docker.com/build/building/best-practices/
- https://cyberpanel.net/blog/docker-multi-stage-builds
- https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/
- https://labs.iximiuz.com/tutorials/docker-multi-stage-builds
- https://www.cherryservers.com/blog/docker-multistage-build
- https://www.blacksmith.sh/blog/understanding-multi-stage-docker-builds
- https://overcast.blog/building-efficient-multi-stage-dockerfiles-for-production-055f34c4baed

