# Istio Service Mesh

## Spesifikasi Cluster 
### Azure Kubernetes Service 
- 2 Node
- 2 VPU
- 8 GB RAM

# Install Istio

## Download and install istio's binary file
```bash
curl -L https://istio.io/downloadIstio | sh -
```
## Install the Istio Operator
```bash
istioctl operator init  
kubectl get all -n istio-operator
```
## Apply istio
```bash
kubectl create ns istio-system
kubectl apply -f istio.yaml
```
## Check if Istio has sucessfully installed
```bash
kubectl get all -n istio-system
```
## Check External IP

# Apply Microservices Application
## Bookinfo Application
Create namespace bookinfo
```bash
kubectl create ns bookinfo
```

Create istio injection label
```bash
kubectl get ns bookinfo --show-labels
kubectl label ns bookinfo istio-injection=enabled
```

# Apply microservice ( Deployment + Service )
```bash
kubectl apply -f bookinfo-app/bookinfo.yaml -n bookinfo
```
## Apply Gateway dan Virtual Service
```bash
kubectl apply -f bookinfo-app/bookinfo-gateway.yaml -n bookinfo
```
## Pastikan Seluruh Komponen Terinstall
```bash
kubectl get all -n bookinfo
kubectl get gateway -n bookinfo
kubectl get virtualservice -n bookinfo
```
Access : 
```bash 
http://<ip-external-istio-ingressgateway>/productpage
```

# Apply Prometheus 

```bash 
kubectl apply -f addons/prometheus.yaml -n istio-system
kubectl get pod -n istio-system
```
# Apply Grafana Dashboard
```bash
kubectl apply -f addons/grafana -n istio-system
```

lihat service grafana
```bash
kubectl get svc grafana -n istio-system
```

kita harus mengganti service grafana agar bisa diakses melalui service loadbalancer

```bash
kubectl edit svc grafana -n istio-system
```

ubah type service ClusterIP menjadi LoadBalancer, lalu cek lagi IP external yang diperoleh

```bash
kubectl get svc grafana -n istio-system
```

akses dashboard grafana melalui IP external yang diperoleh
```bash
http://<ip-external-service-grafana>:3000
```

Dashboard Grafana untuk monitoring service mesh melalui istio sudah siap digunakan

# Apply Kiali Dashboard 
```bash
kubectl apply -f addons/kiali-crd.yaml
kubectl apply -f addons/kiali -n istio-system
```

lihat service kiali
```bash
kubectl get svc kiali -n istio-system
```

kita harus mengganti service kiali agar bisa diakses melalui service loadbalancer

```bash
kubectl edit svc kiali -n istio-system
```

ubah type service ClusterIP menjadi LoadBalancer, lalu cek lagi IP external yang diperoleh

```bash
kubectl get svc kiali -n istio-system
```

akses dashboard grafana melalui IP external yang diperoleh
```bash
http://<ip-external-service-kiali>:20001
```

Dashboard Kiali untuk monitoring service mesh melalui istio sudah siap digunakan

## Testing Inject Traffic 
1. Linux Terminal
```bash
watch -n <jeda waktu> curl -o /dev/null -s -w %{http_code} 192.168.0.101/productpage
```
or 

2. Windows PowerShell
```bash
While ($true) { curl -UseBasicParsing http://192.168.0.101/productpage;Start-Sleep -Seconds <jeda waktu>;} 
```
note: 
- Jeda waktu merupakan jarak waktu antar looping pemberian traffic
- 192.168.0.101 merupakan IP istio ingress gateway 


## Installasi istio dan penggunaanya selesai

source : 
- https://istio.io/latest/docs/setup/install/operator/
- https://istio.io/latest/docs/examples/bookinfo/
- https://metallb.universe.tf/installation/

