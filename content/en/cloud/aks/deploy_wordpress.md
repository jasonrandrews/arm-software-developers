---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Deploy WordPress Example"
type: docs
weight: 2
hide_summary: true
description: >
    Learn how to deploy WordPress example.
---

## Prerequisites

* [An AKS cluster](/content/en/cloud/aks/cluster_deployment.md)

## Deploy the AKS cluster

The Kubernetes yamls we show below are a modified version of the [Kubernetes WordPress Tutorial](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/) in the Kubernetes documentation. We found that running this tutorial as-is does not work. Therefore, we suggest using our modified version of these yamls.

We use three yaml files to deploy WordPress: kustomization.yaml, mysql-deployment.yaml, and wordpress-deployment.yaml.

Add the following code in **kustomization.yaml** file:

```console
secretGenerator:
- name: mysql-pass
  literals:
  - password=YourPasswordHere
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
```

Add the following code in **mysql-deployment.yaml** file:

```console
apiVersion: v1
kind: Service
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  clusterIP: None
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: managed-csi
  resources:
    requests:
      storage: 20Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: mysql
    spec:
      containers:
      - image: mysql:8.0.30
        name: mysql
        env:
        - name: MYSQL_DATABASE
          value: wordpressdb
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        - name: MYSQL_USER
          value: mysqluser
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
```

Add the following code in **wordpress-deployment.yaml** file:

```console
apiVersion: v1
kind: Service
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  type: LoadBalancer
  loadBalancerSourceRanges: ["0.0.0.0/0"]
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wp-pv-claim
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: managed-csi
  resources:
    requests:
      storage: 20Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:6.0.2-apache
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: wordpress-mysql
        - name: WORDPRESS_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        - name: WORDPRESS_DB_NAME
          value: wordpressdb
        - name: WORDPRESS_DB_USER
          value: mysqluser
        ports:
        - containerPort: 80
          name: wordpress
        volumeMounts:
        - name: wordpress-persistent-storage
          mountPath: /var/www/html
      volumes:
      - name: wordpress-persistent-storage
        persistentVolumeClaim:
          claimName: wp-pv-claim
```

Now apply the configuration by running the following command:

```console
kubectl apply -k ./
```

Check on the volume claims by running the following command:

```console
kubectl get pvc
```

![volume_screenshot](https://user-images.githubusercontent.com/67620689/200744736-3ff29b97-fa8f-4170-ab64-623f683beb53.PNG)

Check on the WordPress and MySQL pods by running the following command:

```console
kubectl get pods
```

![pods_screenshot](https://user-images.githubusercontent.com/67620689/200744412-d6772971-e8bd-4e30-bc89-4f59e06d40a4.PNG)

Now that the pods are running, we can verify that the persistent volumes have been attached by running the following command:

```console
kubectl get volumeattachments
```

![attach_vol_screenshot](https://user-images.githubusercontent.com/67620689/200745055-af49fcad-0d7b-4100-b3a5-7c64cdd996d5.PNG)

To get the external IP address of the WordPress deployment run the following command:

```console
kubectl get svc
```

![ip_screenshot](https://user-images.githubusercontent.com/67620689/200745202-973893d4-2455-47a6-9297-2c30b75b358d.PNG)

Now use the external IP and open it in the browser. WordPress welcome screen will be displayed in the browser.

![homescreen_screenshot](https://user-images.githubusercontent.com/67620689/200745521-1e004de9-f982-4b6d-b7e7-638569da2aec.PNG)

[<-- Return to Learning Path](/content/en/cloud/aks/#sections)
