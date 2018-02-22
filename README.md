# k8s-prometheus-grafana-gke
Google K8S Engine. Monitoring with Prometheus and Grafana. Using Prometheus Operator by CoreOS

## GKE INIT
First, we need to configure **kubectl**.
```bash
gcloud container clusters get-credentials <cluster_name> --zone <cluster_zone> --project <project_name>
```
