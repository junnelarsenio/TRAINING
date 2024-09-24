# Virtual Machines Vs Docker Containers
- Docker Containers are not Virtual Machines
- Virutal machine starts in minutes while Docker starts in just about a milliseconds


#### Virtual Machines
- Infrastructure - this can be your laptop, a dedicated server or a Virtual Private server
- Host Operating System - on your laptop this can be MacOs, Window or Linux
- Hypervisor - 2 types of hypervisors
  - Type 1: Direct link to the infrastructure - Hyperkit(OSX) / Hyper-V(Win)
  - Type 2: Runs as an app on the host OS - VirtualBox / VMWare Workstation
- Guest OS -> Binary/Library -> App
- Starts in minutes

#### Docker Containers
- Infrastructure - like VM, this could be your laptop or your server that running in the cloud
- Host Operating System - MacOs, Windows or Linux
- Docker Daemon
- Binary & Library -> App
- Starts in milliseconds
