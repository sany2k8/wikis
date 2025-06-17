## Step-by-Step Guide to Use Docker Secrets for Sensitive Data

### 1. Understand Docker Secrets

- Docker Secrets allow you to securely store sensitive data (passwords, API keys, certificates) and provide them only to containers that need them.
- Secrets are encrypted at rest and in transit within a Docker Swarm cluster.
- Secrets are mounted inside containers as files in `/run/secrets/<secret_name>` (Linux) or `C:\ProgramData\Docker\secrets` (Windows).
- Secrets are only accessible to services explicitly granted access, and only while the container is running.

---

### 2. Initialize Docker Swarm (if not already)

Docker Secrets require running in Swarm mode:

```bash
docker swarm init
```


---

### 3. Create a Secret

You can create a secret from a file or from standard input.

- From a file:

```bash
docker secret create my_secret ./secret_file.txt
```

- From standard input:

```bash
echo "my_password" | docker secret create my_secret -
```


---

### 4. List Existing Secrets

To see all secrets stored in the swarm:

```bash
docker secret ls
```


---

### 5. Inspect a Secret's Metadata

To view details (not the secret content) of a secret:

```bash
docker secret inspect my_secret
```


---

### 6. Use Secrets in a Service

When creating or updating a service, specify which secrets it can access:

```bash
docker service create --name my_service --secret my_secret my_image
```

Or update an existing service to add a secret:

```bash
docker service update --secret-add my_secret my_service
```


---

### 7. Access Secrets Inside the Container

Inside the container, secrets are available as files at `/run/secrets/<secret_name>`.

Example: To read the secret in a container:

```bash
cat /run/secrets/my_secret
```


---

### 8. Remove Secrets

You cannot remove a secret that is currently in use by a running service. First, remove the secret from all services, then delete it:

```bash
docker secret rm my_secret
```


---

### 9. Best Practices

- Use secrets for all sensitive data instead of environment variables or embedding in images.
- Add secrets to `.gitignore` if stored locally to avoid committing sensitive data.
- Use consistent secret names across environments with different values.
- Rotate secrets regularly by creating new secrets with versioned names and updating services.
- Design your applications to read secrets from the filesystem (`/run/secrets/`) rather than environment variables.

---

### Summary Table

| Step | Command / Description |
| :-- | :-- |
| Initialize Swarm | `docker swarm init` |
| Create Secret | `docker secret create <name> <file>` or from stdin |
| List Secrets | `docker secret ls` |
| Inspect Secret | `docker secret inspect <name>` |
| Create Service with Secret | `docker service create --secret <name> ...` |
| Update Service to Add Secret | `docker service update --secret-add <name> ...` |
| Access Secret in Container | Read file at `/run/secrets/<name>` |
| Remove Secret | `docker secret rm <name>` (only if not in use) |


---

Docker Secrets provide a secure, encrypted, and runtime-only way to manage sensitive data in containerized applications running on Docker Swarm, preventing exposure in images, environment variables, or source code.

### References
- https://docs.docker.com/engine/swarm/secrets/

- https://spacelift.io/blog/docker-secrets

- https://semaphoreci.com/blog/docker-secrets-management

- https://labex.io/tutorials/docker-how-to-use-docker-secret-create-command-to-manage-sensitive-data-555220

- https://blog.gitguardian.com/how-to-handle-secrets-in-docker/

- https://beaglesecurity.com/blog/article/secrets-in-docker.html

- https://www.youtube.com/watch?v=SHD8Bl0jEfE

