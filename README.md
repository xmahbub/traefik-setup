# traefik-setup

kubectl create ns traefik
kubectl apply -f resource-quota.yaml -n traefik

#changing context
kubectl config set-context --current --namespace=traefik

#install traefik 
helm repo add traefik https://traefik.github.io/charts
helm repo update

#create secrate 
kubectl apply -f acme-dns-credentials.yml

#install
helm install traefik traefik/traefik --values=traefik-values.yml
