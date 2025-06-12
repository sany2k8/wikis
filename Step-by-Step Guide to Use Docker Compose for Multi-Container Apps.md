## Step-by-Step Guide to Use Docker Compose for Multi-Container Apps

### 1. Install Docker and Docker Compose

- Ensure Docker Engine and Docker Compose are installed on your system.
- On Docker Desktop (Windows/macOS), Docker Compose is included.
- On Linux, install Docker Compose separately if needed.

---

### 2. Create Your Project Structure

Organize your files, for example:

```
my-app/
  ├── backend/
  │    ├── Dockerfile
  │    └── app.js
  ├── docker-compose.yml
```


---

### 3. Write Dockerfiles for Each Service

Example for a Node.js backend (`backend/Dockerfile`):

```dockerfile
FROM node:lts-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```


---

### 4. Define Services in `docker-compose.yml`

Create `docker-compose.yml` in the project root:

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

- `backend` service builds from the `backend` folder.
- `mongo` service uses the official MongoDB image.
- `depends_on` ensures MongoDB starts before backend.
- Volume persists MongoDB data.

---

### 5. Start the Multi-Container Application

Run the following command in the project root:

```bash
docker compose up -d --build
```

- `-d` runs containers in detached mode.
- `--build` builds images before starting.

---

### 6. Verify Running Containers

Check running containers:

```bash
docker compose ps
```

View logs:

```bash
docker compose logs -f
```


---

### 7. Stop and Remove Containers

To stop and remove containers, networks, and volumes:

```bash
docker compose down
```


---

### 8. Advanced Tips

- **Networking:** Services in the same Compose file share a default network and can communicate via service names (e.g., `mongo`).
- **Environment Variables:** Use `environment:` in `docker-compose.yml` to pass variables.
- **Scaling:** Scale services with:

```bash
docker compose up -d --scale backend=3
```

- **Multiple Compose Files:** Use overrides for different environments:

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```


---

### Summary Table

| Step | Command / File Example |
| :-- | :-- |
| Write Dockerfiles | `backend/Dockerfile` |
| Define Compose File | `docker-compose.yml` |
| Build \& Start | `docker compose up -d --build` |
| List Containers | `docker compose ps` |
| View Logs | `docker compose logs -f` |
| Stop \& Remove | `docker compose down` |
| Scale Services | `docker compose up -d --scale backend=3` |


---

Using Docker Compose simplifies managing multi-container apps by defining all services, networks, and volumes in one YAML file, replacing complex `docker run` commands with easy orchestration.

<div style="text-align: center">⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ Always Sany ⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂</div>

[^1]: https://docs.docker.com/get-started/docker-concepts/running-containers/multi-container-applications/

[^2]: https://dev.to/mukhilpadmanabhan/a-simple-guide-to-docker-compose-multi-container-applications-5e0g

[^3]: https://www.ionos.com/digitalguide/server/configuration/docker-compose-tutorial/

[^4]: https://www.datacamp.com/tutorial/docker-compose-guide

[^5]: https://docs.docker.com/get-started/workshop/07_multi_container/

[^6]: https://www.youtube.com/watch?v=23ij4bub_Hw

[^7]: https://learn.microsoft.com/en-us/dotnet/architecture/microservices/multi-container-microservice-net-applications/multi-container-applications-docker-compose

[^8]: https://labex.io/tutorials/docker-how-to-configure-and-manage-multi-container-docker-applications-393009

