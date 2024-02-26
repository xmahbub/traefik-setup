<h1 align="center">
      Traefik Kubernetes Setup
</h1>


### Clone the repo

```
git clone https://github.com/xmahbub/traefik-setup.git
cd traefik-setup
```

### Creating Namespace
```
kubectl create ns traefik
```
### Creating Resource Quota (Optional)

```
kubectl apply -f resource-quota.yaml -n traefik
```

### Changing context
```
kubectl config set-context --current --namespace=traefik
```
### Add healm repo and Update 
```
helm repo add traefik https://traefik.github.io/charts
helm repo update
```
### Create secrate for Acme DNS Challenge

Acme DNS will work for everyone no need any extra config just apply my config. This secrate will work for everyone.

```
kubectl apply -f acme-dns-credentials.yml
```

### Pre-Check uninstall helm from kube-system
```
helm uninstall traefik -n kube-system
```

### Install Traefik 
```
helm -n traefik install traefik traefik/traefik --values=traefik-values.yml
```


# Create application name space
 kubectl create ns applications

# Chnaging contex to application
kubectl config set-context --current --namespace=applications

# cd into application-deployment 
cd application-deployment 

kubectl apply -f nginx-pvc.yaml

kubectl apply -f nginx-deployment-service-ingress.yml

kubectl exec -it nginx-7667fc87d8-4b4tr -- /bin/bash

cd /usr/share/nginx/html

echo "hello" > index.html


kubectl exec -it traefik-6489b845bd-km5rv -- /bin/sh

cd ssl-certs

cat acme-dns.json

{"mahbub.securedsoft.online":{"fulldomain":"bf63a32a-3f5d-4d4c-affb-3a8361e60443.auth.acme-dns.io","subdomain":"bf63a32a-3f5d-4d4c-affb-3a8361e60443","username":"43247a42-a64a-4cc5-ab76-1e8cedc668bf","password":"AyaaSGh1Y7TSd_pPTO-JnUO5cuWIHGqbM9iuI3ua","server_url":"https://auth.acme-dns.io"}}


CREATE DNS RECORD

CNAME  Record
 target 
_acme-challenge.mahbub.securedsoft.online

value
bf63a32a-3f5d-4d4c-affb-3a8361e60443.auth.acme-dns.io

A Record

34.x.x.11 (Traefik loadbelancer IP) 
mahbub.securedsoft.online

If certificate is not valid just restart traefik once 

kubectl rollout restart deployment traefik -n traefik



✌🏻😎
