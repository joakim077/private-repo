Tasks:
Ingress: with minikube
HPA, VPA: Add resources request, limit -> 
HELM: super eassy
## 2. Horizontal Pod Autoscaler
- To work with HPA you need Metrics Server deployed and configured. 
- The Kubernetes Metrics Server collects resource metrics from the kubelets in your cluster, and exposes those metrics through the Kubernetes API.
- Based on Resource utilization metrics and configuration defined on HPA spec it scale-out and scale-in you application.
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
edit the deployment metrics-server to work without TLS.

```bash
kubectl edit deployments.apps -n kube-system metrics-server 

# add 
# --kubelet-insecure-tls
# to spec/template/spec/containers/0/args/
```
Create HPA for autoScaling your application.
```bash
kubectl apply -f hpa.yaml
```

Create a pod for generating load and testing
```bash
kubectl run -i --tty load-generator --image=busybox /bin/sh

while true; do wget -q -O- http://bankapp-service.default.svc.cluster.local; done
```
check newly created pods
```bash
watch -n2 kubectl get pods -n bankapp-namespace
```
kubectl patch deployment my-deployment -p '[{"op": "add", "path": "/spec/template/spec/containers/0/env/-", "value": "my-value"}]'


## 2. Vertical Pod Autoscaler
- It scale-up and scale down the request of resources (CPU, memory) depending on the workload.
- It will set the resource request automatically bases on usage for proper scheduling.
- In case of limits defined in template of containers, it also manges a ration between request/limit.
VPA is installed in k8s using Custom Resource Definition (CRD).

Install CRD using command below.
```bash 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/vpa-release-1.0/vertical-pod-autoscaler/deploy/vpa-v1-crd-gen.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/vpa-release-1.0/vertical-pod-autoscaler/deploy/vpa-rbac.yaml
```
Apply VPA configution
```bash
kubectl apply -f vpa.yaml
```

Generate load to application and check resource utilization.
```bash
kubectl run -i --tty load-generator --image=busybox /bin/sh

while true; do wget -q -O- http://bankapp-service.default.svc.cluster.local; done
```

```bash
kubectl top nodes

kubectl describe deployment bankapp-deployment -n bankapp-namespace
```