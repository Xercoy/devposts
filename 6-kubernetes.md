# Development Environment Setup

In a development environment, Kubernetes runs as a tool called [`MiniKube`](https://github.com/kubernetes/minikube) and works in conjunction with a VM `provider(?)`. My choice is `VirtualBox`.

**Prerequisities**

- `VirtualBox` of course

- `kubectl`, the Kubernetes CLI, check out the docs [here](https://kubernetes.io/docs/user-guide/prereqs/). It's as simple as `brew install kubectl`. You could also download it via curl. This also sticks the binary in `/usr/local/bin`:
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
```

**Installation**

- Use the curl command found in the docs. It will also move the binary to `/usr/local/bin`:
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.18.0/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

**Check if successful** - run `minikube start` to kick things off. There should be messages indicating progress + completion. There's also a simple hello world type exercise that can be done, take a look at the [README](https://github.com/kubernetes/minikube/blob/v0.18.0/README.md) for more information.

Much more detailed usage information can be found on the getting started page [here](https://kubernetes.io/docs/getting-started-guides/minikube/#instructions).

## Deployments

**Creating a Deployment** - See [here](https://kubernetes.io/docs/tutorials/stateless-application/run-stateless-application-deployment/) for more info. 

Create a Deployment from an image, no `YAML` file necessary : 
```
$ kubectl run <name of deployment> --image=<image name>:<version tag>
# verify with kubectl get pods
```

Or alternatively with a `YAML` file:
```

```


## Pods

**Creating a Pod**

A `YAML` file is the format used to specify the characteristics of a Pod.

`$ kubectl create -f <PATH TO YAML FILE>`

