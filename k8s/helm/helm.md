## HELM: Package manager for K8s

- helm architecture

- helm directory structure

#### Installing Helm

```bash
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

    chmod 700 get_helm.sh

    ./get_helm.sh
```


#### Getting Started

- Terminologies:
- basics
    ```bash
        helm repo add stable https://charts.helm.sh/stable
    ```

#### Run SpringBoot Bank Application with helm

Create secret
```bash
kubectl create secret generic mysql-secret \
    --from-literal=MYSQL_ROOT_PASSWORD=Test@123 \
    --from-literal=SPRING_DATASOURCE_PASSWORD=Test@123 \
    --namespace my-namespace
```
**NOTE** make sure you create the secret in same namespace which you have created through values.yml

Deploy the bankapp using HELM
```bash 
helm install <release-name> bankapp/
```

Happy Helming!


## ITs "{{ Values.name }}-stirng"
 
## Metrics server, VPA must be installed first  CRD

## Secret 