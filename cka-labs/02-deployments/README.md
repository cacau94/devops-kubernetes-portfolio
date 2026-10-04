\# Lab 02 - Kubernetes Deployments and ReplicaSets



\## Objective



Practice creating and managing Kubernetes Deployments, ReplicaSets, scaling, rolling updates, and rollbacks.



\## Environment



\- Kubernetes v1.37.1

\- Two-node cluster

\- Namespace: `cka-practice`

\- Application: Nginx



\## Create Deployment



```bash

kubectl create deployment web-deployment \\

&#x20; --image=nginx:stable \\

&#x20; --replicas=2 \\

&#x20; -n cka-practice

