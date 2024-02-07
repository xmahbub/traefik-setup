# traefik setup for K8S / Kubernetes

# Creating Namespace
```
kubectl create ns traefik
```
# Creating Resource Quota (Optional)

```
kubectl apply -f resource-quota.yaml -n traefik
```

# Changing context
```
kubectl config set-context --current --namespace=traefik
```
# Add healm repo and Update 
```
helm repo add traefik https://traefik.github.io/charts
helm repo update
```
# Create secrate for Acme DNS Challenge

# Acme DNS will work for everyone no need any extra config just apply my config. This secrate will work for everyone.

```
kubectl apply -f acme-dns-credentials.yml
```

# install (Finnaly install traefik)
```
helm install traefik traefik/traefik --values=traefik-values.yml
```