# 🚀 Kubernetes Application Deployment and Rolling Update

## 📌 Project Overview

This project demonstrates the deployment of a containerized web application on **Kubernetes** using a Deployment and a LoadBalancer Service.

A Kubernetes Deployment is used to manage multiple replicas of the application, providing scalability and high availability.

A Kubernetes LoadBalancer Service is used to expose the application externally.

The project also demonstrates **Rolling Updates, rollout history, and rollback** by changing the container image and managing different versions of the application.

---

## 🎯 Project Objectives

* Deploy a containerized web application on Kubernetes.
* Create a Kubernetes Deployment using a YAML manifest.
* Run multiple replicas of the application.
* Expose the application using a LoadBalancer Service.
* Perform a Rolling Update by changing the container image.
* Monitor the rollout status.
* View Deployment rollout history.
* Roll back to a previous application version.
* Verify application availability after updates and rollback.

---

## 🏗️ Architecture

```text
                    Kubernetes Cluster
                           |
                           |
                    Deployment
                 zomato-deployment
                           |
                    replicas: 3
                           |
              ┌────────────┼────────────┐
              |            |            |
             Pod          Pod          Pod
              |            |            |
              └────────────┼────────────┘
                           |
                           v
                   LoadBalancer Service
                    zomato-service
                           |
                           v
                    External Access
```

---

## 🛠️ Technologies Used

| Technology             | Purpose                                 |
| ---------------------- | --------------------------------------- |
| Kubernetes             | Container orchestration                 |
| Kubernetes Deployment  | Manage application replicas and updates |
| Kubernetes Service     | Expose the application                  |
| LoadBalancer           | External application access             |
| Docker Container Image | Application container                   |
| YAML                   | Kubernetes configuration                |

---

## 📁 Project Structure

```text
kubernetes-rolling-update/
│
├── README.md
│
└── manifests/
    └── zomato-deployment-service.yaml
```

---

## 📄 Kubernetes Manifest

The project uses a single YAML manifest containing:

1. Kubernetes Deployment
2. Kubernetes LoadBalancer Service

### Deployment Configuration

The Deployment creates **3 replicas** of the application.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: zomato-deployment
  labels:
    app: food
spec:
  replicas: 3
  selector:
    matchLabels:
      app: food
  template:
    metadata:
      labels:
        app: food
    spec:
      containers:
        - name: zomato-container
          image: kastrov/zomato
          ports:
            - containerPort: 3000
```

### Service Configuration

The application is exposed externally using a Kubernetes **LoadBalancer Service**.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: zomato-service
spec:
  type: LoadBalancer
  selector:
    app: food
  ports:
    - port: 80
      targetPort: 3000
```

---

## 🚀 Deployment

Apply the Kubernetes manifest:

```bash
kubectl apply -f zomato-deployment-service.yaml
```

Check the Deployment:

```bash
kubectl get deployments
```

Check the Pods:

```bash
kubectl get pods
```

Check the Service:

```bash
kubectl get svc
```

The LoadBalancer Service provides an external endpoint through which the application can be accessed.

---

## 🔄 Rolling Update

A Rolling Update allows a new version of the application to be deployed gradually while existing Pods are replaced.

The container image can be changed using:

```bash
kubectl set image deployment/zomato-deployment zomato-container=NEW_IMAGE
```

Check the rollout status:

```bash
kubectl rollout status deployment/zomato-deployment
```

Check the Pods during or after the update:

```bash
kubectl get pods
```

Kubernetes gradually replaces the existing Pods with Pods running the new image.

---

## 📜 Rollout History

Kubernetes maintains the revision history of the Deployment.

View the rollout history:

```bash
kubectl rollout history deployment/zomato-deployment
```

This can be used to identify previous Deployment revisions.

---

## ↩️ Rollback

If a new application version needs to be reverted, the Deployment can be rolled back to the previous revision.

```bash
kubectl rollout undo deployment/zomato-deployment
```

Verify the rollback:

```bash
kubectl rollout status deployment/zomato-deployment
```

Then check the Pods:

```bash
kubectl get pods
```

---

## 🔍 Application Verification

After deployment, rolling update, or rollback, verify the application using:

```bash
kubectl get pods
kubectl get svc
```

The application can be accessed using the external endpoint provided by the LoadBalancer Service.

---

## 📚 Key Kubernetes Concepts Demonstrated

* Kubernetes Deployment
* Replica-based application deployment
* Kubernetes Pods
* Kubernetes Services
* LoadBalancer Service
* Rolling Updates
* Deployment revisions
* Rollout history
* Rollback
* Container image updates
* External application access

---

## ✅ Project Outcome

This project demonstrates how Kubernetes can be used to deploy and manage a containerized web application using a Deployment and Service.

The application runs with multiple replicas for scalability and availability and is exposed externally through a LoadBalancer Service.

The project also demonstrates application version updates using a Rolling Update strategy and the ability to roll back to a previous Deployment revision when required.

---

## 📸 Project Evidence

Screenshots will be added after the practical environment is recreated.

Planned screenshots include:

* Kubernetes Deployment
* Running Pods
* LoadBalancer Service
* Application accessed through the external endpoint
* Image update
* Rolling Update status
* Rollout history
* Rollback
* Application verification after rollback
