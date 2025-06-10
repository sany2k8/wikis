## Step-by-Step Guide: Build and Push a Docker Image to a Docker Registry

**Pre-requisites:**

- Docker installed on your machine
- Account on Docker Hub or another Docker registry

---

### 1. Write a Dockerfile

Create a `Dockerfile` in your project directory. Example:

```Dockerfile
FROM nginx
RUN echo "<h1>Hello world from Docker!</h1>" > /usr/share/nginx/html/index.html
```

This uses the official Nginx image and customizes the homepage[^2][^5].

---

### 2. Build the Docker Image

Open a terminal in your project directory and run:

```bash
docker build -t <your-docker-username>/my-nginx-image:latest .
```

Replace `<your-docker-username>` with your Docker Hub username. This command builds the image and tags it for your registry[^2][^4][^5].

---

### 3. Test the Image Locally (Optional)

Run the image to make sure it works:

```bash
docker run -p 8080:80 --rm <your-docker-username>/my-nginx-image:latest
```

Visit `http://localhost:8080` to check the result[^2][^5].

---

### 4. Log In to the Docker Registry

Authenticate with Docker Hub (or your registry):

```bash
docker login
```

Enter your Docker Hub username and password when prompted[^2][^3][^4].

For a private registry, use:

```bash
docker login myregistry.example.com
```

And provide your credentials[^3].

---

### 5. Tag the Image (If Needed)

If you want to push to a different registry or repository, tag the image:

```bash
docker tag <local-image>:latest <registry-url>/<repo>/<image>:<tag>
```

Example for Docker Hub:

```bash
docker tag my-nginx-image:latest <your-docker-username>/my-nginx-image:latest
```

Example for a private registry:

```bash
docker tag my-nginx-image:latest myregistry.example.com/my-nginx-image:latest
```


---

### 6. Push the Image to the Registry

Push the image to Docker Hub (or your registry):

```bash
docker push <your-docker-username>/my-nginx-image:latest
```

For a private registry:

```bash
docker push myregistry.example.com/my-nginx-image:latest
```


---

### 7. Verify the Image in the Registry

- Go to your Docker Hub account or your registry's web interface.
- Check that your image appears in your repositories[^2][^5].

---

**Summary Table**


| Step | Command/Action |
| :-- | :-- |
| Write Dockerfile | Create `Dockerfile` in project directory |
| Build Image | `docker build -t <username>/image:tag .` |
| Test Image | `docker run -p 8080:80 --rm <username>/image:tag` |
| Login | `docker login` (or `docker login <registry-url>`) |
| Tag Image | `docker tag <image>:tag <registry-url>/<repo>/<image>:tag` (if needed) |
| Push Image | `docker push <username>/image:tag` (or to your registry URL) |
| Verify | Check registry UI for your image |


---

This process works for Docker Hub and any Docker-compliant registry, including private registries[^3][^4][^8].

<div style="text-align: center">⁂</div>

[^1]: https://docs.gitlab.com/user/packages/container_registry/build_and_push_images/

[^2]: https://docs.docker.com/docker-hub/quickstart/

[^3]: https://cyberpanel.net/blog/docker-push-image-to-registry

[^4]: https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image/

[^5]: https://www.stacksimplify.com/aws-eks/docker-basics/build-docker-image/

[^6]: https://developer.harness.io/docs/continuous-integration/use-ci/build-and-upload-artifacts/build-and-push/build-and-push-to-docker-registry/

[^7]: https://support.atlassian.com/bitbucket-cloud/docs/build-and-push-a-docker-image-to-a-container-registry/

[^8]: https://docs.docker.com/reference/cli/docker/image/push/

[^9]: https://docs.docker.com/get-started/introduction/build-and-push-first-image/

[^10]: https://github.com/docker/build-push-action

