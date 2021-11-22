# Linkerd Service Mesh

## Spesifikasi Cluster 
### Azure Kubernetes Service 
- 2 Node
- 2 VPU
- 8 GB RAM

# Install Linkerd
## Download and install linkerd's binary file
```bash
curl -fsL https://run.linkerd.io/install | sh
```
## Verify Linkerd Version
```bash
linkerd version
```
## Validate Kubernetes Cluster
```bash
linkerd check --pre
```
## Install Control Plane 
```bash
linkerd install | kubectl apply -f -
```
## Verify Linkerd Control Plane
```bash
linkerd check
```
# Install Demo Application
Let’s install a demo application called Emojivoto. Emojivoto is a simple standalone Kubernetes application that uses a mix of gRPC and HTTP calls to allow the user to vote on their favorite emojis.
```bash
curl -fsL https://run.linkerd.io/emojivoto.yml | kubectl apply -f -
``` 
## Port Forward web-svc
```bash
kubectl -n emojivoto port-forward svc/web-svc 8080:80
```
### Check the web in browser
```bash
localhost:8080
```
## Deploy Mesh
```bash
kubectl get -n emojivoto deploy -o yaml \
  | linkerd inject - \
  | kubectl apply -f -
```
## Check Data Plane
```bash
linkerd -n emojivoto check --proxy
```
# Explore Linkerd
  - The viz extension, which will install an on-cluster metric stack; or
  - The buoyant-cloud extension, which will connect to a hosted metrics stack.
  
You can install either or both extensions

## Viz Dashboard
```bash
linkerd viz install | kubectl apply -f - # install the on-cluster metrics stack
```

open viz dashboard
```bash
linkerd viz dashboard &
```

## Buoyant Dashboard
```bash
curl -fsL https://buoyant.cloud/install | sh # get the installer
linkerd buoyant install | kubectl apply -f - # connect to the hosted metrics stack
```
open buoyant dashboard
```bash
linkerd viz dashboard &
```