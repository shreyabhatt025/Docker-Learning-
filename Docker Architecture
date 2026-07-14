
# Docker Architecture

Docker follows a **client-server architecture**. When we run a Docker command, several components work together to create and manage containers.

## Overall Architecture

```text
                    User
                      │
                      │ docker run nginx
                      ▼
             +------------------+
             | Docker CLI       |
             | (Docker Client)  |
             +------------------+
                      │
          REST API Request
                      │
                      ▼
             +------------------+
             | Docker Daemon    |
             | (dockerd)        |
             +------------------+
                      │
                      ▼
             +------------------+
             | containerd       |
             +------------------+
                      │
                      ▼
             +------------------+
             | runc             |
             +------------------+
                      │
                      ▼
              Linux Kernel
                      │
                      ▼
                 Container
```

---

# Components

## 1. Docker Client (Docker CLI)

The Docker Client is the interface through which users interact with Docker.

Whenever we execute commands like:

```bash
docker run ubuntu
docker ps
docker images
docker stop container_id
```

the Docker CLI sends these requests to the Docker Daemon using the Docker REST API.

**Responsibilities**

* Accepts user commands
* Sends requests to Docker Daemon
* Displays the output to the user

---

## 2. Docker Daemon (dockerd)

Docker Daemon is the main background service responsible for managing Docker objects.

It continuously runs in the background and listens for requests from the Docker Client.

**Responsibilities**

* Build Docker images
* Create containers
* Start and stop containers
* Remove containers
* Manage Docker networks
* Manage Docker volumes

The Docker Daemon does **not directly create containers**. Instead, it delegates this task to **containerd**.

---

## 3. containerd

containerd is a container runtime responsible for the complete lifecycle of containers.

It receives requests from Docker Daemon and performs operations such as:

* Creating containers
* Starting containers
* Stopping containers
* Deleting containers

---

## 4. runc

runc is a lightweight runtime that actually creates the container.

It communicates directly with the Linux Kernel and sets up:

* Process isolation
* Filesystem isolation
* Network isolation
* Resource limits

Once everything is configured, the container starts running.

---

## 5. Linux Kernel

The Linux Kernel is the core of the operating system.

Containers do **not have their own kernel**.

Instead, all containers share the **Host OS Kernel**.

The kernel provides container isolation using Linux features like:

* Namespaces
* cgroups (Control Groups)

This is why containers are lightweight compared to Virtual Machines.

---

# Request Flow

Suppose the following command is executed:

```bash
docker run nginx
```

The execution flow is:

```text
User
   │
   ▼
Docker CLI
   │
   ▼
Docker Daemon
   │
   ▼
containerd
   │
   ▼
runc
   │
   ▼
Linux Kernel
   │
   ▼
Container Starts
```

---

# Docker Desktop

Docker Desktop is a graphical application that includes Docker Engine and provides an easy-to-use interface.

It allows users to:

* View running containers
* View Docker images
* Monitor resource usage
* Manage volumes
* Manage networks
* View logs

Docker Desktop is mainly used on Windows and macOS, where it also provides the Linux environment required to run Linux containers.

---

# Key Points

* Docker uses a **client-server architecture**.
* Docker CLI is used to send commands.
* Docker Daemon manages Docker resources.
* containerd manages the lifecycle of containers.
* runc creates the actual container process.
* Containers share the Host Operating System's Kernel.
* Since containers do not include a separate operating system, they are lightweight and start much faster than Virtual Machines.

---

## Quick Revision

| Component      | Purpose                                               |
| -------------- | ----------------------------------------------------- |
| Docker CLI     | Accepts user commands                                 |
| Docker Daemon  | Manages Docker resources and receives client requests |
| containerd     | Manages the container lifecycle                       |
| runc           | Creates the isolated container process                |
| Linux Kernel   | Provides process isolation and resource management    |
| Docker Desktop | GUI for managing Docker (primarily on Windows/macOS)  |

> **Interview Tip:** A common misconception is that Docker Daemon directly creates containers. In reality, the daemon delegates container creation to **containerd**, which then uses **runc** to interact with the Linux Kernel and create the container. This separation of responsibilities makes Docker modular and easier to maintain.
