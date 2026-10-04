# Lab 03 - Kubernetes Services

## Objective

Create a Kubernetes ClusterIP Service and verify communication with backend Pods using both the Service IP and DNS name.

## Environment

- Kubernetes v1.37.1
- Two-node cluster
- Namespace: cka-practice
- Deployment: web-deployment
- Service: web-service

## Create the Service

Command used:

kubectl expose deployment web-deployment --name=web-service --port=80 --target-port=80 --type=ClusterIP -n cka-practice

Result:

The service web-service was created successfully.

## Verify the Service

Commands used:

kubectl get services -n cka-practice

kubectl describe service web-service -n cka-practice

The Service was created as a ClusterIP service.

Service details:

Name: web-service

Type: ClusterIP

Cluster IP: 10.106.242.123

Port: 80/TCP

Target Port: 80/TCP

Selector:

app=web-deployment

The selector matched the Pods created by web-deployment.

## Verify Backend Endpoints

Command used:

kubectl get endpoints web-service -n cka-practice

Result:

The Service discovered the backend Pods successfully.

The output showed four Pod endpoints listening on port 80.

Example:

192.168.1.196:80

192.168.1.246:80

192.168.1.27:80

and one additional endpoint.

Note:

Kubernetes v1.37 displayed a warning that the legacy Endpoints API is deprecated and EndpointSlice should be used for newer environments.

## Test the ClusterIP

Command used:

curl -I http://10.106.242.123

Result:

HTTP/1.1 200 OK

Server: nginx/1.30.5

This confirmed that the ClusterIP Service successfully routed traffic to the backend Nginx Pods.

## Test Kubernetes Service Discovery

A temporary client Pod was created to test access using the Service DNS name.

Command used:

kubectl run test-client --image=curlimages/curl:latest --restart=Never -n cka-practice -- sleep 3600

Verify the client Pod:

kubectl get pods -n cka-practice

The test-client Pod reached Running status.

Test Service access by DNS name:

kubectl exec -n cka-practice test-client -- curl -I http://web-service

Result:

HTTP/1.1 200 OK

This confirmed that Kubernetes DNS successfully resolved the Service name web-service and routed traffic to the backend Pods.

## Traffic Flow

The communication path tested in this lab was:

test-client Pod

-> Kubernetes DNS

-> web-service

-> ClusterIP

-> backend Nginx Pods

## Service Manifest

The Service manifest used for this lab is saved as:

service.yaml

Content:

apiVersion: v1
kind: Service
metadata:
  name: web-service
  namespace: cka-practice
spec:
  selector:
    app: web-deployment
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP

## What I Practiced

- Creating a Kubernetes ClusterIP Service
- Understanding Service selectors
- Connecting a Service to Deployment Pods
- Inspecting Service configuration
- Checking backend endpoints
- Understanding the relationship between Services and Pods
- Testing ClusterIP connectivity
- Creating a temporary client Pod
- Using Kubernetes DNS for service discovery
- Testing Pod-to-Service communication
- Verifying HTTP connectivity through a Service

## Status

Completed