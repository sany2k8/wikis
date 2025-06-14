## Step-by-Step Guide to Use Docker Volumes for Persistent Storage

### 1. Understand Docker Volumes

- Volumes are Docker-managed persistent storage that exist outside the container’s writable layer, ensuring data persists even if containers are removed or recreated[^1][^5][^6].
- They are stored on the Docker host (usually under `/var/lib/docker/volumes/` on Linux) and are isolated from the host filesystem, unlike bind mounts[^1][^5].
- Volumes are preferred for data persistence because they are easier to back up, migrate, and share among containers[^1][^6].
- Use volumes when you want Docker to manage data storage and do not need direct host access to files.

---

### 2. Create a Docker Volume

Create a named volume explicitly:

```bash
docker volume create my_volume
```

List existing volumes:

```bash
docker volume ls
```

Inspect volume details:

```bash
docker volume inspect my_volume
```


---

### 3. Run a Container with the Volume Attached

Mount the volume inside the container to persist data at a specific path:

```bash
docker run -d \
  --name my_container \
  -v my_volume:/path/in/container \
  my_image
```

**Example:** Running PostgreSQL with persistent data:

```bash
docker run -d \
  --name my_postgres \
  -e POSTGRES_PASSWORD=mysecretpassword \
  -v pg_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres
```

This mounts the `pg_data` volume to the directory where PostgreSQL stores its data, ensuring data persists across container restarts or removals[^2][^4].

---

### 4. Verify Data Persistence

- Create or modify data inside the container.
- Stop and remove the container:

```bash
docker stop my_postgres
docker rm my_postgres
```

- Start a new container with the same volume:

```bash
docker run -d \
  --name new_postgres \
  -v pg_data:/var/lib/postgresql/data \
  postgres
```

- The data remains intact and accessible in the new container[^2].

---

### 5. Share Volumes Between Containers

Mount the same volume into multiple containers to share data:

```bash
docker run -d -v my_volume:/data container1
docker run -d -v my_volume:/data container2
```

Docker manages synchronization between containers accessing the same volume[^5][^6].

---

### 6. Remove Volumes

- Remove a volume only if it is not in use by any container:

```bash
docker volume rm my_volume
```

- Remove all unused volumes to free space:

```bash
docker volume prune
```


---

### 7. Best Practices

- Use named volumes for important persistent data like databases or user files[^6].
- Avoid bind mounts in production unless you need direct host access[^1][^6].
- Backup volumes by running a temporary container that mounts the volume and copies data out.
- Monitor volume usage and clean unused volumes regularly[^5].
- Use volumes to improve performance and portability compared to writing data inside containers[^1].

---

### Summary Table

| Step                      | Command / Description                                 |
| :------------------------ | :---------------------------------------------------- |
| Create volume             | `docker volume create my_volume`                      |
| List volumes              | `docker volume ls`                                    |
| Inspect volume            | `docker volume inspect my_volume`                     |
| Run container with volume | `docker run -v my_volume:/path/in/container my_image` |
| Stop \& remove container  | `docker stop <container>` and `docker rm <container>` |
| Reuse volume              | Attach same volume to new container                   |
| Share volume              | Mount same volume to multiple containers              |
| Remove volume             | `docker volume rm my_volume`                          |
| Remove unused volumes     | `docker volume prune`                                 |


---

Using Docker volumes ensures your container data is safely persisted beyond container lifecycles, improving reliability and enabling easier data sharing and backup in containerized environments[^1][^2][^5][^6].

**⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂ References *⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂⁂**

[^1]: https://docs.docker.com/engine/storage/volumes/

[^2]: https://docs.docker.com/get-started/docker-concepts/running-containers/persisting-container-data/

[^3]: https://spacelift.io/blog/docker-volumes

[^4]: https://www.kdnuggets.com/how-to-use-docker-volumes-for-persistent-data-storage

[^5]: https://www.tutorialspoint.com/docker/docker_volumes.htm

[^6]: https://www.linkedin.com/pulse/docker-volumes-ultimate-guide-persistent-data-storage-amit-rautela-my1xc

[^7]: https://docs.docker.com/engine/storage/

[^8]: https://labex.io/tutorials/docker-how-to-configure-the-storage-location-for-docker-volumes-416179

