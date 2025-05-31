# Prometheus & Grafana Dashboard 

This project demonstrates how I implemented Prometheus & Grafana Dashboard using **AWS**, **Docker**, **Kubernetes**, **Kind**, **Helm**, **Prometheus**, **Grafana**.

---

## What I Did

1. **Created an instance in AWS**  
   Created a `instance` in `AWS` and connected with the it's terminal using SSH client Key.

2. **Install Docker, Kind**  
   ### Installed Docker & Kind:
   Docker Install & adding the user to the group:
   ```bash
    sudo apt get update
    sudo apt install docker.io
    sudo usermod -aG docker $USER && newgrp docker
   ```
   ### Kind Install:
   Inside the `install_kind.sh` command for installing the kind
   ```bash
   chmod +x install_kind.sh
   ./install_kind.sh
   ```

   ### Kubectl Install:
   Inside the `install_kubectl.sh` command for installing the kind
   ```bash
   chmod +x install_kubectl.sh
   ./install_kubectl.sh
   ```



3. **Created a kind cluster with 2 Worker Node**  
    ### Node creation:
    ```bash
    kubectl apply -f config.yml
    ```

4. **Helm Install**  

    ### Installation of Helm:
    ```bash
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    chmod +x get_helm.sh
    ./get_helm.sh
    ```


5. **Prometheus Install**  

    ### Installation of Prometheus
    ```bash
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

    helm repo add stable https://charts.helm.sh/stable

    helm repo update

    kubectl create namespace monitoring

    helm install kind-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set prometheus.service.type=NodePort --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set alertmanager.service.nodePort=32000 --set alertmanager.service.type=NodePort --set prometheus-node-exporter.service.nodePort=32001 --set prometheus-node-exporter.service.type=NodePort

    kubectl get svc -n monitoring

    kubectl get namespace
    ```

6. ** Forwording the port of Prometheus **

    ```bash 
    kubectl port-forward svc/kind-prometheus-kube-prome-prometheus -n monitoring 9090:9090 --address=0.0.0.0
    ```

7. ** Forwording the port of Grafana **

    ```bash 
    kubectl port-forward svc/kind-prometheus-grafana -n monitoring 3000:80 --address=0.0.0.0
    ```

## Demo ##


🎥 [Click here to view the demo](https://drive.google.com/file/d/1S2KeLMxp8uePqu8EHbCvmIGPTVUd_YbF/view?usp=sharing)

## Author 
Symon


Learning Docker + Kubernetes — One Pod at a Time 🚢☸️