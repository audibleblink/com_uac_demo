class: center, middle, inverse
# Containers
[and managing them with Docker]
.footnote[View source on [GitHub](https://github.com/audibleblink/containers-intro)]

---
layout: false
class: center, middle

# Works on my machine ¯\_(ツ)_/¯
.footnote[-- Developers.]

---
class: inverse

.left-column[
# [Agenda](#)
]

.right-column[

  .right[

# Containers
# Namespaces
# CGroups
# Docker
# DEMO!
  ]
]

???
* really quick intro to Containers

---
class: center, middle, inverse
# Containers
### [[What](#) are they?]

---

.left-column[
# What is it?
]

.right-column[
# A logical unit of Linux kernel features
.paragraph[
Containers are processes

Distributed as tarballs

Anchored to namespaces

Controlled by CGroups
]
]

---

.left-column[
# What's a Namespace
]

## Additional Flags Passed to Process-Creation Syscalls
.right-column[

When creating a process, you can restrict what this process can see
and what other processes can see about it

.paragraph[
- Hostname
- Process IDs
- Filesystems
- IPC
- Networking
- User IDs
]


]

---
class: center, middle, inverse
# Control Groups
### [[aka](#) CGroups]

---

.left-column[
# What's a CGroup
]

## Access Controls and Limitation of Resources
.right-column[

### Resource limiting  
  Groups can be set to not exceed a configured memory limit
### Prioritization  
  Some groups may get a larger share of CPU or disk I/O
### Accounting  
  Measures a group's resource usage
### Control  
  Freezing groups of processes

]

---

.left-column[
# What's a CGroup
]

# What Can We Control?

.paragraph[
-  Memory  
`/sys/fs/cgroup/memory`
- CPU/Cores  
`/sys/fs/cgroup/cpu*`
- I/O  
`/sys/fs/cgroup/blkio`
- Processes  
`/sys/fs/cgroup/cgroup.procs`
- Devices  
`/sys/fs/cgroup/devices.*`
]
---
class: center, middle, inverse
# Docker

---

# As Containers Are To Docker

--
.right[
# JPEGs are to Photoshop
# MP3 are to Audacity
# PDFs are to Acrobat Pro
# Trees are to Git
]

---

.left-column[
# The Dockerfile
]

.right-column[
# Instructions for making a Docker Image

```
FROM alpine:3.7

# Install packages
RUN echo 'http://dl-4.alpinelinux.org/alpine/edge/testing' >> \
  /etc/apk/repositories && \
  apk --no-cache add openvpn dante-server supervisor && \
  rm -rf /var/cache/

# Add image configuration and scripts
ADD VPN /VPN
ADD etc/ /etc/

EXPOSE 1080
CMD ["supervisord","-n"]
```
]

---
.left-column[
# Images
]

.right-column[
# Templates From Which One Makes Containers

## Building a New Image
```
> sudo docker build --tag demo .

```

## Listing Built Images

```
> sudo docker images

```

## More Commands

```
> docker help build

> docker help images
```
]
---

.left-column[
# Containers
]

.right-column[

# Deltas from Images

## Creating a Container

```
> sudo docker run --name demo_1 demo [command]
```

## Run Container and Attach

```
> sudo docker run -it --rm --name demo_1 demo /bin/bash
```

## List All Container

```
> sudo docker ps -a
```

## More Commands

```
> docker help run
```
]


---

.left-column[
# Containers
]

.right-column[

Containers can be stopped and restarted.

## Restarting a Stopped Container

```
# Find the stopped container ID
> sudo docker ps -a

# Find the stopped container ID
> sudo docker start -i <ID>
```

## Executing a Command in a Running Container

```
> sudo docker exec -it <ID> bash
```

## More Commands

```
> docker help exec
```
]


---
class: center, middle, inverse
# Demo
### [[Practical](#) Application]
