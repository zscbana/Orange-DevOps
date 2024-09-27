# Setup Jenkins On Kubernetes

## 1- Create a Namespace

- Kubernetes Jenkins Deployment
```
kubectl create namespace devops-tools
```

## 2- Create a 'serviceAccount.yaml' file and copy the following admin service account manifest.

- Check serviceAccount.yaml File 

```
omarelbanna@Omars-MacBook-Air Project % kubectl apply -f serviceAccount.yaml
clusterrole.rbac.authorization.k8s.io/jenkins-admin created
serviceaccount/jenkins-admin created
clusterrolebinding.rbac.authorization.k8s.io/jenkins-admin created
```

## Step 3: Create 'volume.yaml' and copy the following persistent volume manifest.

- Check volume.yaml File

```
omarelbanna@Omars-MacBook-Air Project % kubectl create -f volume.yaml
storageclass.storage.k8s.io/local-storage created
persistentvolume/jenkins-pv-volume created
persistentvolumeclaim/jenkins-pv-claim created
```

## Step 4: Create a Deployment file named 'deployment.yaml' and copy the following deployment manifest.

- Check deployment.yaml File
