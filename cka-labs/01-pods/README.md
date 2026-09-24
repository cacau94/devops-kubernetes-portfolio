# Lab 01 — Pod basics

## Goal
Create an nginx Pod and verify that it serves HTTP.

## Commands
kubectl create namespace cka-practice
kubectl run web --image=nginx:stable --port=80 -n cka-practice
kubectl get pod web -n cka-practice -o wide
kubectl describe pod web -n cka-practice
kubectl logs web -n cka-practice
kubectl exec -n cka-practice web -- curl -I http://localhost:80

## Result
Both cluster nodes were Ready. The `web` Pod was scheduled on `node01`.
The first check showed `ContainerCreating` while the image was being pulled.
It then became `1/1 Running` with zero restarts.
An HTTP request from inside the container returned `HTTP/1.1 200 OK`.

## Troubleshooting note
`wget` was unavailable in the nginx image, so I used the available `curl`
command to verify the HTTP response.
