---
titile: k8s
layout: post
---

[edit k8s](https://github.com/haiy/haiy.github.io/edit/master/k8s.md)
[self](https://haihome.top/k8s)

### Refs
* https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands


========


```bash

#bash complete
echo "source <(kubectl completion bash)" >> ~/.bashrc
## If running Bash 3.2 included with macOS
brew install bash-completion
## or, if running Bash 4.1+
brew install bash-completion@2


docker build -t hello-node:v1 .
kubectl get deployments
kubectl get events
kubectl get pods
kubectl get services
kubectl get deployments
docker rmi hello-node:v1 hello-node:v2 -f
kubectl delete service hello-node
kubectl delete deployment hello-node
kubectl run hello-node --image=hello-node:v1 --port=8080
kubectl expose deployment hello-node --type=LoadBalancer
kubectl config view

#更新配置
kubectl apply -f test.yaml
```
