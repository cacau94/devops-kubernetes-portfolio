# Lab 02 - Kubernetes Deployments and ReplicaSets

## Objective

Practice creating and managing Kubernetes Deployments, ReplicaSets, scaling, rolling updates, and rollbacks.

## Environment

- Kubernetes v1.37.1
- Two-node cluster
- Namespace: cka-practice
- Application: Nginx

## Create Deployment

Command used:

kubectl create deployment web-deployment --image=nginx:stable --replicas=2 -n cka-practice

## Verify Deployment

Commands used:

kubectl get deployments -n cka-practice

kubectl get replicasets -n cka-practice

kubectl get pods -n cka-practice -o wide

Result:

The Deployment created one ReplicaSet and two Nginx Pods.

## Scale Deployment

Command used:

kubectl scale deployment web-deployment --replicas=4 -n cka-practice

Result:

The Deployment successfully scaled from 2 replicas to 4 replicas.

READY: 4/4

AVAILABLE: 4

## Rolling Update

The Nginx image was updated from nginx:stable to nginx:1.29.

Command used:

kubectl set image deployment/web-deployment nginx=nginx:1.29 -n cka-practice

Rollout status:

kubectl rollout status deployment/web-deployment -n cka-practice

Result:

The update completed successfully.

A new ReplicaSet was created and the previous ReplicaSet was scaled down to zero.

## Rollback

View rollout history:

kubectl rollout history deployment/web-deployment -n cka-practice

Rollback command:

kubectl rollout undo deployment/web-deployment -n cka-practice

Verify rollback:

kubectl rollout status deployment/web-deployment -n cka-practice

kubectl get replicasets -n cka-practice

kubectl get pods -n cka-practice

Result:

The previous ReplicaSet was restored to 4 replicas.

The newer ReplicaSet was scaled down to 0 replicas.

## What I Practiced

- Creating Kubernetes Deployments
- Understanding the Deployment and ReplicaSet relationship
- Scaling application replicas
- Performing rolling updates
- Checking rollout status
- Viewing rollout history
- Rolling back application changes
- Verifying Pods after deployment changes

## Status

Completed