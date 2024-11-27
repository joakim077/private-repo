- Tasks:
- Ingress: with minikube
- HPA, VPA: Add resources request, limit -> 
- HELM: super eassy
kubectl get svc -n ingress-nginx

If you are Using cloud provider managed kubernetes cluster, it will create a service of type LoadBalancer.
add the public DNS of of ELB, an ELB will be created, edit the ingress.
 

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: bankapp-ingress
  namespace: bankapp-namespace
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: af48c3fa7f50b45d69360e00d2f78b86-1460831707.ap-south-1.elb.amazonaws.com  # Add here you Public DNS name of ELB
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: bankapp-service
            port:
              number: 8080

```

