
Software packages that contain a App and all dependencies for the container Apps to run.  Multiple Apps can be run in a single container, but their is not how containers are usually used.  

![[Container.PNG]]

Containers are run on a **Container Engine** (Docker Engine)

Lightweight and include only the dependencies require to run the specific App

**Container Orchestrator** - Software Platform automating the deployment, management, scaling of containers.  
	Ex. Kubernetes - Designed by Google
		Docker Swarm

In small numbers manual operation is possible, but large-scale system (Microservices) can require thousands of containers

**Microservices Architecture** - Is an approach to software architecture that divides a larger solution into smaller parts(microservices) Those microservices all run in containers that can be orchestrated by Kubernetes (or another platform)

##### VMs or Containers


| VM                             | Containers                                                                 |
| ------------------------------ | -------------------------------------------------------------------------- |
| - Minutes to Boot              | + Milliseconds to boot                                                     |
| - Take up more disk space (GB) | + Little disck space (MB)                                                  |
| - Use more CPU/RAM             | + Little CPU/RAM                                                           |
| - Portable                     | + More portable                                                            |
| + More isolated                | - Less isolated.  All run on the same OS.  If OS crashes, all are affected |

