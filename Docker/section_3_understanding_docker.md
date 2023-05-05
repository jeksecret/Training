# Insights on this Section
- Docker containers are not VMs.
- Docker can run on dedicated hardware.
- VMs isolate systems while Docker isolates application.
#### Virtual Machines:
- Infrastructure>host operating system>hypervisor>guest os>binaries & libraries>app
#### Docker Containers:
- Infrastructure>host operating system>docker daemon>binaries & libraries>app

> #### 2 types of hypervisor
1. direct link to the infrastructure *e.g* Hyperkit (OSX) / Hyper-v (Win)
2. runs as an app on the host OS *e.g* Virtual Box /VMWare workstation
