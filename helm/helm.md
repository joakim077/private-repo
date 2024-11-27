# HELM 
**NOTE** This Helm chart assumes that you already have installed following things in your cluster
- Ingress CRD
    ```bash
        helm upgrade --install ingress-nginx ingress-nginx \
            --repo https://kubernetes.github.io/ingress-nginx \
            --namespace ingress-nginx --create-namespace
    ```
- Metrics Server for HPA
    ```bash
        helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
        helm upgrade --install metrics-server metrics-server/metrics-server

        # add 
        # --kubelet-insecure-tls
        # to spec/template/spec/containers/0/args/
    ```
- VPA CRD.
    ```bash
        kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/vpa-release-1.0/vertical-pod-autoscaler/deploy/vpa-v1-crd-gen.yaml

        kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/vpa-release-1.0/vertical-pod-autoscaler/deploy/vpa-rbac.yaml
    ```

## Run the SpringBoot Bankapp using helm
```bash
    helm install <release-name> bankapp/
    helm install banakapp-release1 bankapp/
```


## HELM: Package manager for K8s

- helm architecture

- helm directory structure

## Installing Helm

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
Create secret
```bash
kubectl create secret generic mysql-secret \
    --from-literal=MYSQL_ROOT_PASSWORD=Test@123 \
    --from-literal=SPRING_DATASOURCE_PASSWORD=Test@123 \
    --namespace bankapp-namespace
```
Happy Helming!


 ------------------------------------------------------------------------------
  ------------------------------------------------------------------------------
   ------------------------------------------------------------------------------
    ------------------------------------------------------------------------------
     ------------------------------------------------------------------------------
      ------------------------------------------------------------------------------
      
## Metrics server, VPA must be installed first  CRD

## Secret creaeted manually and update spec secret


## secret ingress namespace delete
## namespace file delete, but values m hai

## Secret -> not encoded
## INGRESS valid DNS

