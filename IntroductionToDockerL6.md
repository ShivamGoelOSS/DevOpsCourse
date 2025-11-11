**1. What is Docker?**
* Docker is a platform to package and run applications inside *containers*.
* A container includes:
  * code
  * runtime
  * libraries
  * system tools
  * configuration
* This makes the app run the **same everywhere** (laptop, server, cloud).

**2. Why Docker?**
*Before Docker:*
* Apps installed directly on OS.
* Dependency/version conflicts.
* Repeating setup on every new machine.

*With Docker:*
* Each app runs in its own container (isolated).
* No conflicts.
* Easy to run, stop, copy, delete.
* Environment stays consistent.

**3. Important Concepts**
* **Image** → Template/blueprint used to create containers.
* **Container** → Running instance of an image.
* **Dockerfile** → Instructions to build an image.
* **Docker Engine** → Builds and runs containers.
* **Docker Hub** → Public repository for images.
* **Docker Compose** → Runs multi-container apps using `docker-compose.yml`.

**4. Docker Architecture**
* You use **Docker CLI** to give commands.
* CLI talks to **Docker Daemon** (background service).
* Daemon manages:
  * images
  * containers
  * networks
  * storage
* Everything runs on the **host OS**.

**5. Installing Docker**
* Linux quick install:

  ```
  sudo apt update
  sudo apt install docker.io -y
  sudo systemctl enable docker
  sudo systemctl start docker
  ```
* Verify:

  ```
  docker --version
  docker run hello-world
  ```

**6. Basic Docker Commands**
* Check version → `docker --version`
* Test Docker → `docker run hello-world`
* List running containers → `docker ps`
* List all containers → `docker ps -a`
* List images → `docker images`
* Pull image → `docker pull nginx`
* Run Ubuntu shell → `docker run -it ubuntu bash`
* Stop container → `docker stop <id>`
* Remove container → `docker rm <id>`
* Remove image → `docker rmi <id>`
---

**7. What is a Docker Image?**
* A read-only, layered template that contains everything needed for the app.

**8. Image Layers**
* Each Dockerfile instruction creates a new layer:
  * `FROM` → base layer
  * `RUN` → new layer
  * `COPY` → new layer
  * `CMD` → metadata layer

**9. Container Layers**
* Images = read-only layers.
* Container adds **one writable layer** on top.
* Changes are stored only in this writable layer (copy-on-write).

**10. Where Images Are Stored (Linux)**
* Path: `/var/lib/docker/overlay2`
* Contains:
  * `diff/` → actual changed files
  * `lower/` → parent layers
  * `work/` → temp area

**11. Inspecting Layers**
* Show layers:
  `docker image inspect <image>`
* Show build history:
  `docker history <image>`

**12. Layer Reuse (Caching)**
* Docker identifies layers via SHA256 hashes.
* Reuses identical layers across images.
* Makes builds faster and saves disk.

