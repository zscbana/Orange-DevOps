# Week 03 Project: Jenkins on Kubernetes (Minikube) for CI/CD Pipeline

This project aims to set up Jenkins inside a Kubernetes (Minikube) environment, which will be used to deploy the Kubernetes deployments created in **Week 02**. The Week 02 project involved creating Kubernetes deployments for an application with three tiers (Proxy, Backend, and Database), each scaled with two replicas for high availability. The focus of this week is to automate the deployment process using Jenkins as a Continuous Integration and Continuous Deployment (CI/CD) tool.

---

## 1. Project Overview

The goal of this project is to automate the deployment process of the Kubernetes-based application that was built in **Week 02**. In Week 02, we created Kubernetes deployments for the Proxy, Backend, and Database tiers of the application, ensuring they were scalable and highly available with two replicas for each tier. The primary focus of this week is to set up a Jenkins server inside Minikube and configure it to trigger CI/CD pipelines for automated deployments to the Kubernetes cluster.

### **Week 02 Project Recap:**
In the previous week (Week 02), the project involved creating the following Kubernetes resources:
- **Proxy**: A service that acts as a gateway for routing traffic.
- **Backend**: The application logic and business layer.
- **Database**: The persistent storage layer, typically using a service like PostgreSQL or MySQL.

The goal of Week 02 was to ensure each of these application tiers was highly available and scalable within Kubernetes.

### **Week 03 Objective:**
This week, we will set up Jenkins as a CI/CD tool to automate the deployment of these three tiers onto the Kubernetes environment using Jenkins pipelines.

---

## 2. Prerequisites

Before setting up Jenkins in Minikube, ensure you have the following:

- **Minikube** installed and running (used to create a local Kubernetes cluster).
- **kubectl** installed to interact with the Kubernetes cluster.
- **Jenkins** (latest stable version) to automate the CI/CD pipeline.
- Access to the **Week 02 Kubernetes deployment YAML files** for Proxy, Backend, and Database services.

---

## 3. Setting Up Minikube

1. **Install Minikube**: Follow the official documentation to install Minikube for your operating system.
2. **Start Minikube**: Run the following command to start the Minikube cluster:
    ```bash
    minikube start
    ```
3. **Check Cluster Status**: Verify the cluster is running with:
    ```bash
    kubectl cluster-info
    ```
    
## Step 4: Create a Dockerfile that installs Jenkins and kubectl:
```
# Start with the official Jenkins image
FROM jenkins/jenkins:lts

# Set environment variables
ENV KUBECTL_VERSION=v1.26.0
ENV KUBECTL_BINARY=kubectl

# Switch to root user to install kubectl
USER root

# Install necessary packages and kubectl
RUN apt-get update && \
    apt-get install -y curl && \
    curl -LO "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/${KUBECTL_BINARY}" && \
    chmod +x ${KUBECTL_BINARY} && \
    mv ${KUBECTL_BINARY} /usr/local/bin/ && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Switch back to the Jenkins user
USER jenkins

# Expose Jenkins port
EXPOSE 8080

# Start Jenkins
ENTRYPOINT ["jenkins.sh"]
```
- docker build -t omarj .


- docker tag omarj <your-dockerhub-username>/omarj

- docker push <your-dockerhub-username>/omarj
- kubectl create namespace devops-tools

## Create serviceAccount.yaml

```---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: jenkins-admin
rules:
  - apiGroups: [""]
    resources: ["*"]
    verbs: ["*"]
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins-admin
  namespace: devops-tools
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: jenkins-admin
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: jenkins-admin
subjects:
- kind: ServiceAccount
  name: jenkins-admin
  namespace: devops-tools
```

- kubectl apply -f serviceAccount.yaml -n devops-tools

## Create Volume.yaml
```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: local-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: jenkins-pv-volume
  labels:
    type: local
spec:
  storageClassName: local-storage
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain  # Optional: Defines what happens to the PV when released
  local:
    path: /mnt  # Make sure this path exists on the Minikube VM
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - minikube  # This should match the node name in Minikube
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: jenkins-pv-claim
  namespace: devops-tools
spec:
  storageClassName: local-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```
- kubectl apply -f volume.yaml -n devops-tools

## Step 5: Create Jenkins Deployment

``` apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins
  namespace: devops-tools
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins-server
  template:
    metadata:
      labels:
        app: jenkins-server
    spec:
      securityContext:
            fsGroup: 1000
            runAsUser: 1000
      serviceAccountName: jenkins-admin
      containers:
        - name: jenkins
          image: omarbanna/omarj
          resources:
            limits:
              memory: "2Gi"
              cpu: "1000m"
            requests:
              memory: "500Mi"
              cpu: "500m"
          ports:
            - name: httpport
              containerPort: 8080
            - name: jnlpport
              containerPort: 50000
          livenessProbe:
            httpGet:
              path: "/login"
              port: 8080
            initialDelaySeconds: 90
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 5
          readinessProbe:
            httpGet:
              path: "/login"
              port: 8080
            initialDelaySeconds: 60
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
          volumeMounts:
            - name: jenkins-data
              mountPath: /var/jenkins_home
      volumes:
        - name: jenkins-data
          persistentVolumeClaim:
              claimName: jenkins-pv-claim
```
- kubectl apply -f deployment.yaml -n devops-tools

## Step 6: Expose Jenkins

- kubectl expose deployment jenkins --type=NodePort --name=jenkins-service -n devops-tools

## Step 6: Access Jenkins
- minikube service jenkins-service -n devops-tools --url

## Step 8: Verify Deployment
- kubectl get pods -n devops-tools

- kubectl exec -it <jenkins-pod-name> -n devops-tools -- /bin/bash

 - cat /var/jenkins_home/secrets/initialAdminPassword

## step 9 Create a Role: This role will allow the jenkins-admin service account to perform actions on the deployments and services in the webapp namespace.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: webapp
  name: jenkins-deployment-role
rules:
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["get", "list", "watch", "create", "update", "delete"]
- apiGroups: [""]
  resources: ["services"]
  verbs: ["get", "list", "watch", "create", "update", "delete"]
```

## Create a RoleBinding: This will bind the Role to the jenkins-admin service account.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: jenkins-deployment-binding
  namespace: webapp
subjects:
- kind: ServiceAccount
  name: jenkins-admin
  namespace: devops-tools # Update with your actual namespace where the service account is located
roleRef:
  kind: Role
  name: jenkins-deployment-role
  apiGroup: rbac.authorization.k8s.io
```
- Apply the Role and RoleBinding: Use the following commands to apply these files:
- kubectl apply -f role.yaml
- kubectl apply -f rolebinding.yaml

## Verify the Permissions: After applying the Role and RoleBinding, you can verify the permissions by running:
- kubectl auth can-i get deployments --as=system:serviceaccount:devops-tools:jenkins-admin -n webapp

- This command checks if the service account has permission to get deployments in the webapp namespace. If it returns yes, the permissions are set correctly.

## run the pipeline

```
pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/zscbana/Orange-DevOps'
        NAMESPACE = 'webapp'
    }
    stages {
        stage('Clone Repository') {
            steps {
                // Cloning the GitHub repository
                git url: "${REPO_URL}", branch: 'main'
            }
        }
        stage('Navigate and List Files') {
            steps {
                // List files and navigate to the project directory
                sh '''
                ls
                cd Week02/Project
                ls
                '''
            }
        }
        stage('Start Deployment') {
            steps {
                // Execute the Start script for deploying the app
                sh './Week02/Project/Start'
            }
        }
    }
    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
```
```
omarelbanna@Omars-MacBook-Air test2 % kubectl get pods -n webapp
NAME                                 READY   STATUS                       RESTARTS   AGE
backend-deployment-6b7867797-h62hd   1/1     Running                      0          41m
backend-deployment-6b7867797-p9qml   1/1     Running                      0          41m
database-deployment-58c9dcbb-qr6wv   1/1     Running                      0          41m
proxy-deployment-795d645db-6vwq9     1/1     Running                      0          41m
proxy-deployment-795d645db-hvx2s     1/1     Running                      0          41m
```
---

## 8. Conclusion

This project demonstrates how to automate the deployment of a multi-tier application using Jenkins and Kubernetes (Minikube). By setting up Jenkins in a Kubernetes environment, we created an efficient CI/CD pipeline for the deployment of services with high availability and scalability.

---

## 9. References

- Jenkins Documentation: [https://www.jenkins.io/doc/](https://www.jenkins.io/doc/)
- Kubernetes Documentation: [https://kubernetes.io/docs/](https://kubernetes.io/docs/)
