




This guide is to setup and use Docker in Docker on QuickPod Community Cloud

Docker in Docker  needs privileged pods/containers, Quickpod provides priviliged containers along with regular unprivileged containers to be able to use Docker In Dockeer (DIND) you have to select a privileged container

Privileged containers are only available for GPU pod types, you can filter for privileged containers on the top right of the GPU search page, look for the orange privileged flag on top of the offer

![image](https://github.com/user-attachments/assets/8400aa1a-114a-440a-bcda-09cacc4326ec)

QuickPod provides a ubuntu 22.04 based dind template but you can use any ubuntu template to use Docker in Docker, we are exposing  the host docker socket to the privileged pods

![image](https://github.com/user-attachments/assets/4408ea02-aa59-4386-8675-df54439f02bd)

Select a privileged pod and choose Ubuntu DIND template and create POD

You can check docker availabilty witth command docker ps or docker info

systemctl will not work in dind, neither will service docker commands because we are using the host docker daemon

once inside the container you can test docker in docker by creating a pod as follows

docker run -it --runtime=nvidia --gpus all ubuntu /bin/bash

The nvidia runtime is preinstalled, so are some essential packages like nvcc, nvtop, git etc.

For port forwarding you will have to figure out the host open ports which are sequential e.g. if ssh port is 40000, then 40001 onwards are available

the same port you will forward while creating a sub pod as follows

docker run -it --runtime=nvidia --gpus all -p 40001:22 -p 40002:80 -p 40003:443 ubuntu /bin/bash

IMPORTANT: /workspace on host is mapped to /workspace on container, so you should run all your programs etc inside the /workspace folder, this is to facilitate any volume mappings your docker compose files will like to do

Please open a ticket in discord if you face problems


