# Prometheus-Grafana

1️⃣ Verify prerequisites
```bash
kubectl get nodes
helm version
kubectl version --short
```

2️⃣ Add Helm repository
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

3️⃣ Create a dedicated namespace 
```bash
kubectl create namespace monitoring
```
4️⃣ Install Prometheus + Grafana using Helm
Basic install
```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace monitoring
```
5️⃣ Verify all pods
```bash
kubectl get pods -n monitoring
```

6️⃣ Access Grafana UI
Get Grafana password
```bash
kubectl get secret monitoring-grafana -n monitoring \
  -o jsonpath="{.data.admin-password}" | base64 --decode


Username: admin
```

Port-forward Grafana
```bash
kubectl port-forward svc/monitoring-grafana 3000:80 -n monitoring
```
or
```bash
 kubectl port-forward svc/monitoring-grafana  --address 0.0.0.0  3000:80  -n monitoring
```

7️⃣ Access Prometheus UI
```bash
kubectl port-forward svc/monitoring-kube-prometheus-prometheus 9090 -n monitoring
```
or
```bash
kubectl port-forward svc/monitoring-kube-prometheus-prometheus \ 
  --address 0.0.0.0 \
  9090:9090 \
  -n monitoring
```
