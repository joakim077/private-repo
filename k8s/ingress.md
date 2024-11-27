## Ingress
Ingress in Kubernetes is used to route external traffic to the Kubernetes cluster.

Feature of Ingress:
  - Domain-based routing
  - Path-based routing 
  - SSL termination
  - LoadBalancing


Ingress is composed of Ingress Controller and Ingress Resource.
- Ingress Controller: a nginx web server that acts as a proxy server, and forwards traffic into the Kubernetes services based on configuration.
- Ingress Resource: configures the Ingress controller for traffic routing to the Kubernetes services based on domain or path.

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: bankapp-ingress   # Name of ingress 
  namespace: bankapp-namespace  # namespace
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: bank.joakim.online  # Add here you Public DNS name of ELB
    http:
      paths:
      - path: /               # path based routing request to kubernetes service
        pathType: Prefix
        backend:
          service:
            name: bankapp-service    # service to forwarad request
            port:
              number: 8080

```

---

### Exposing Bankapp using Ingress
### 1. In cloud provider Managed Cluster.
- If you are Using cloud provider managed kubernetes cluster, it will create a service of type LoadBalancer, in the namespace ingress-nginx.
- Get the public DNS of LoadBalancer and update the Ingress configuration file, add the Fully Quallified DNS Name in `spec.rules.host`. 
  ```bash
  kubectl edit ingress bankapp-ingress
  ```
- OR if you have domain, Map the domain with your LoadBalancer IP/DNS and add your domain in `spec.rules.host`.
 

### 2.In minikube cluster.
- If you are Using cloud provider managed kubernetes cluster, it will create a service of type LoadBalancer, in the namespace ingress-nginx.
- Get the public DNS of LoadBalancer and update the Ingress configuration file, add the Fully Quallified DNS Name in `spec.rules.host`. 
  ```bash
  kubectl edit ingress bankapp-ingress -n nginx-ingress
  ```
- OR if you have domain, Map the domain with your LoadBalancer IP/DNS and add your domain in `spec.rules.host`.
