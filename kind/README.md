# Kind
## What's Kind ?
- Kind is a tool for running local K8s cluster using Docker container as a **"node"**. We're using Windows 10 for Research and Develop only.

## Prerequisites and Setup
- Docker Desktop - https://www.docker.com/products/docker-desktop/
- Kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

## Install kind for windows using powershell
```
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.12.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
```
ps. installation step 2 you can add path to default environment path to easier to call kind.exe

## Verify kind version 
```
kind.exe version
```

## Create your first cluster
```
kind.exe create cluster --name <your-cluster-name>           # This command use for create default cluster your'll get only 1 Control Plane node
kind.exe get clusters                                        # Get your cluster name information
kubectl get node                                             # Get your online node
docker ps                                                    # Check your node online as a container engine
kind.exe delete cluster --name <your-cluster-name>           # Cleanup 
```

## Create Custom Confugation
Example: kind-example-config.yaml
```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

## Create cluster using custom configuration
```
kind.exe create cluster --name <your-cluster-name> --config lab.yml
kind.exe get clusters
kubectl get node
docker ps
```

## Load your custom image to your cluster
```
docker build -t my-custom-image:unique-tag ./my-image-dir
kind load docker-image my-custom-image:unique-tag
kubectl apply -f my-manifest-using-my-image:unique-tag
```

ref: https://kind.sigs.k8s.io/