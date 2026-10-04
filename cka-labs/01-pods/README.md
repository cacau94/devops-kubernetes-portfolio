# Lab 01 - Kubernetes Pods

## Goal

Create an Nginx Pod and verify that it serves HTTP successfully.

## Environment

- Kubernetes v1.37.1
- Two-node cluster
- Namespace: `cka-practice`
- Pod: `web`
- Image: `nginx:stable`

## Commands

Create the namespace:

```bash
kubectl create namespace cka-practice