## Step-by-Step Guide to Use Docker Networking for Container Communication

### 1. Understand Docker Network Types

Docker supports several network types, each suited for different use cases:

- **bridge** (default): Creates an isolated internal network on the host where containers can communicate by IP or name.
- **host**: Shares the host’s network stack, containers use host’s IP and ports directly (no isolation).
- **none**: Disables networking for the container.
- **overlay**: Enables multi-host container communication in Docker Swarm or multi-node setups.
- **macvlan** and **ipvlan**: Assign containers MAC addresses for full network integration.

---

### 2. Create a User-Defined Bridge Network (Optional but Recommended)

User-defined bridge networks allow easier container name resolution and better isolation than the default bridge.

```bash
docker network create my_bridge_network
```

List networks:

```bash
docker network ls
```


---

### 3. Run Containers on the Same Network

Run containers attached to the same network to enable communication by container name:

```bash
docker run -d --name db --network my_bridge_network postgres
docker run -d --name web --network my_bridge_network my-web-app
```

The `web` container can connect to `db` using hostname `db`.

---

### 4. Connect Existing Containers to Networks

To connect a running container to a network:

```bash
docker network connect my_bridge_network existing_container
```

To disconnect:

```bash
docker network disconnect my_bridge_network existing_container
```


---

### 5. Use Docker DNS for Service Discovery

Containers on the same user-defined network can resolve each other by container name automatically, e.g., `db` resolves to the IP of the `db` container.

Example connection string inside `web` container:

```
postgres://user:password@db:5432/database
```


---

### 6. Use Host Networking Mode (Optional)

For performance-sensitive apps or when you want the container to share the host’s network interface:

```bash
docker run --network host my-container
```

Note: This disables network isolation and can cause port conflicts.

---

### 7. Inspect Network Details

To inspect a network and see connected containers and IPs:

```bash
docker network inspect my_bridge_network
```

To find a container’s IP address:

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name
```


---

### 8. Communicate Across Multiple Networks

Containers can be connected to multiple networks:

```bash
docker network connect network1 container
docker network connect network2 container
```

This allows containers to communicate with different groups of containers securely.

---

### 9. Use Overlay Networks for Multi-Host Communication

In Docker Swarm mode, create an overlay network to enable containers on different hosts to communicate:

```bash
docker network create -d overlay my_overlay_network
```

Deploy services on the overlay network to enable secure multi-host communication.

---

### Summary Table

| Step | Command / Description |
| :-- | :-- |
| Create bridge network | `docker network create my_bridge_network` |
| Run container on network | `docker run --network my_bridge_network ...` |
| Connect existing container | `docker network connect my_bridge_network container` |
| Disconnect container | `docker network disconnect my_bridge_network container` |
| Inspect network | `docker network inspect my_bridge_network` |
| Find container IP | `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container` |
| Use host network | `docker run --network host ...` |
| Create overlay network (Swarm) | `docker network create -d overlay my_overlay_network` |


---

Docker networking abstracts complex Linux networking details, providing seamless container communication with automatic DNS-based service discovery, network isolation, and flexible multi-host capabilities.

### References

- https://spacelift.io/blog/docker-networking

- https://docs.docker.com/engine/network/

- https://dev.to/tusharops_29/docker-networking-basics-network-types-examples-5ed7

- https://www.networkcomputing.com/data-center-networking/docker-networking-fundamentals

- https://betterstack.com/community/guides/scaling-docker/docker-networks/

- https://dockerlabs.collabnix.com/networking/A1-network-basics.html

- https://labs.iximiuz.com/tutorials/container-networking-from-scratch

- https://www.tigera.io/learn/guides/kubernetes-networking/container-networking/

