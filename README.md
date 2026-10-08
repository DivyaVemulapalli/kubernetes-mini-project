# Kubernetes Mini Project

A beginner-level Kubernetes project demonstrating how to deploy and expose a containerized Nginx application using Kubernetes manifests.

## What I Practiced

* Creating Kubernetes Deployment manifests
* Creating Kubernetes Service manifests
* Running multiple Pod replicas
* Using labels and selectors
* Exposing Pods using a ClusterIP Service
* Verifying Pods and Services
* Testing Service-to-Pod connectivity
* Basic Kubernetes troubleshooting
* Scaling a Deployment

## Project Structure

```text
k8s-mini-project/
├── deployment.yaml
├── service.yaml
└── README.md
```

## Kubernetes Resources

### Deployment

The `deployment.yaml` file creates:

* Deployment: `web-deployment`
* Image: `nginx:alpine`
* Replicas: `3`
* Container port: `80`

### Service

The `service.yaml` file creates:

* Service: `web-service`
* Type: `ClusterIP`
* Service port: `80`
* Target port: `80`
* Selector: `app: web`

The Service selects the Pods using the `app: web` label.

## How to Deploy

Apply the Deployment:

```bash
kubectl apply -f deployment.yaml
```

Apply the Service:

```bash
kubectl apply -f service.yaml
```

## Verify the Deployment

Check the Deployment:

```bash
kubectl get deployments
```

Check the Pods:

```bash
kubectl get pods
```

Check the Service:

```bash
kubectl get svc
```

Check the EndpointSlice:

```bash
kubectl get endpointslice
```

## Test Service Connectivity

A temporary BusyBox Pod can be used to test communication with the Service:

```bash
kubectl run test-client --image=busybox:1.36 --rm -it --restart=Never -- wget -qO- http://web-service
```

The Nginx welcome page confirms that the Service can reach the backend Pods.

## Basic Troubleshooting

For a Service connectivity issue, I practiced checking:

1. Whether the Service exists
2. Service selectors
3. Pod labels
4. Service port and targetPort
5. Pod status and readiness
6. EndpointSlice backend addresses

Useful commands:

```bash
kubectl get svc
kubectl describe svc web-service
kubectl get pods --show-labels
kubectl get pods
kubectl get endpointslice
```

## Scaling

The Deployment was initially tested with two replicas and then scaled to three replicas:

```bash
kubectl scale deployment web-deployment --replicas=3
```

Verify the result:

```bash
kubectl get pods
```

## Technologies

* Kubernetes
* Nginx
* YAML
* kubectl
