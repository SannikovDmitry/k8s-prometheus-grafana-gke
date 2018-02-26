# k8s-prometheus-grafana-gke
Google K8S Engine. Monitoring with Prometheus and Grafana. Using Prometheus Operator by CoreOS

## GKE INIT
First, we need to configure **kubectl**.
```bash
gcloud container clusters get-credentials <cluster_name> --zone <cluster_zone> --project <project_name>
```

kubectl create serviceaccount dashboard -n default

kubectl create clusterrolebinding dashboard-admin -n default \
  --clusterrole=cluster-admin \
  --serviceaccount=default:dashboard

kubectl get secret $(kubectl get serviceaccount kube-system:kubernetes-dashboardkubernetes-dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode

kubectl create clusterrolebinding myname-cluster-admin-binding \
  --clusterrole=cluster-admin \
  --user=sdk96mail@gmail.com

kubectl get deploy -n monitoring

kubectl cluster-info

kubectl describe services

kubectl get ingress grafana -n monitoring

kubectl get service

kubectl --namespace=kube-system get all

kubectl --namespace=kube-system describe service grafana-service

---

kubectl apply -f ~/Desktop/docker-spark-hive-zeppelin/kubernetes/hadoop/dns-config-k8s/hadoop-dns-config.yaml

kubectl apply -f ~/Desktop/docker-spark-hive-zeppelin/kubernetes/hadoop/singlenode-k8s/without-pvc/hadoop-kubernetes.yaml

kubectl apply -f ~/Desktop/docker-spark-hive-zeppelin/kubernetes/hadoop/singlenode-k8s/without-pvc/hadoop-env.yaml

kubectl delete -f ~/Desktop/docker-spark-hive-zeppelin/kubernetes/hadoop/singlenode-k8s/without-pvc/hadoop-kubernetes.yaml

---

kubectl delete -f deploy/kube-config/influxdb/

kubectl --namespace=kube-system port-forward po/grafana-74b576fb87-j9q4x 3000:3000

kubectl port-forward -n monitoring prometheus-kube-prometheus-0 9090

ps -ef|grep kubectl 
pkill -f kubectl

kubectl get pods -l app=prometheus -o name | \
	sed 's/^.*\///' | \
	xargs -I{} kubectl port-forward {} 9090:9090

helm install --name prometheus-operator \ --set rbacEnable=true --namespace=monitoring helm/prometheus-operator

# антиошибка helm
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default

kubectl create clusterrolebinding cluster-admin-binding \
--clusterrole cluster-admin --user $(gcloud config get-value account)

export KUBECONFIG=~/.kube/config

kubectl port-forward $(kubectl get pods --selector=app=grafana-74b576fb87-j9q4x -n  monitoring --output=jsonpath="{.items..metadata.name}") -n monitoring 3000

hack/cluster-monitoring/teardown

## Презентация:
https://docs.google.com/presentation/d/1IaBINi-J9a-tko76B5xOMc5Pol84kRqvIip6LmVeHho/edit?usp=sharing
