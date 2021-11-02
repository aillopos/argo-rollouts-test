# Test Argo Rollouts

```bash
curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64
chmod +x ./kubectl-argo-rollouts-darwin-amd64
sudo mv ./kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts
```

## Workflow with Argo Rollouts
### Setup

Deploy Argo Rollout Controller to the cluster
```bash
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```

```bash
$ kubectl get pods -n argo-rollouts
NAME                             READY   STATUS    RESTARTS   AGE
argo-rollouts-699f446586-srvlb   1/1     Running   0          8s
```

### Deploy to Cluster
```bash
kubectl apply -f rollout.yam
kubectl apply -f service.yaml
```

### Canary Deployment
Set a watcher and then rollout a new version
```bash
kubectl argo rollouts get rollout rollouts-demo --watch
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow
```

### Promotion
```bash
kubectl argo rollouts promote rollouts-demo
```
