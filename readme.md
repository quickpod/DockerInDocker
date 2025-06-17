This guide is to setup and use Docker in Docker on QuickPod Community Cloud

Docker in Docker on needs privileged pods/containers, Quickpod provides priviliged containers along with regular unprivileged containers to be able to use Docker In Dockeer (DIND) you have to select a privileged container

Privileged containers are only available for GPU pod types, you can filter for privileged containers on the top right of the GPU search page, look for the orange privileged flag on top of the offer

![image](https://github.com/user-attachments/assets/8400aa1a-114a-440a-bcda-09cacc4326ec)

QuickPod provides two templates one alpine OS based and another ubuntu 22.04 based

![image](https://github.com/user-attachments/assets/4408ea02-aa59-4386-8675-df54439f02bd)

For most cases Ubuntu template is better suited

Select a privileged pod and choose Ubuntu DIND template and create POD

You can check docker availabilty witth command docker ps or docker info

systemctl will not work in dind, instead use service command, the service name for docker service is supervisor

service supervisor stop/start/restart

once inside the container you can test docker in docker by creating a pod as follows

docker run -it --runtime=nvidia --gpus all ubuntu /bin/bash

The nvidia runtime is preinstalled, so are some essential packages like nvcc, nvtop, git etc.

For port forwarding you will have to forward the port in quickpod before hand with the following docker options

-p 22:22 -p 80:80 -p 443:443

the same port you will forward while creating a sub pod as follows

docker run -it --runtime=nvidia --gpus all -p 22:22 -p 80:80 -p 443:443 ubuntu /bin/bash

Please open a ticket in discord if you face problems


