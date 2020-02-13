---
layout: page
title: DEVOPS Challenges - Развернуть GO приложение в kubernetes с использованием облаков Digital Ocean (По шагам из видео)
description: Задача - Развернуть GO приложение в kubernetes с использованием облаков Digital Ocean (По шагам из видео)
keywords: devops, challenge, kubernetes, go, digital ocean
permalink: /challenges/devops/digital-ocean-kubernetes-go-application/
---

# [DEVOPS Challenges] Challenge 0.1 - Развернуть GO приложение в kubernetes с использованием облаков Digital Ocean (По шагам из видео)

**Задача:**  
Развернуть Go приложиение в kubernetes с использованием облаков Digital Ocean

Желательно использовать свой docker registry (hub.docker.com, quay.io)

<br/>

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/g_-U5jddSuM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>



<br/>

### Шаги по разворачиванию приложения в kubernetes кластере

<br/>

    $ mv k8s-1-16-6-do-0-fra1-1581274701235-kubeconfig.yaml ~/.kube/config

<br/>

    $ kubectl get nodes
    NAME                  STATUS   ROLES    AGE   VERSION
    pool-zueheo387-vd46   Ready    <none>   31s   v1.16.6
    pool-zueheo387-vd4l   Ready    <none>   42s   v1.16.6
    pool-zueheo387-vd4t   Ready    <none>   49s   v1.16.6


<br/>


```yaml
$ cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: go-web-application
spec:
  replicas: 3
  selector:
    matchLabels:
      name: go-web-app
  template:
    metadata:
      labels:
        name: go-web-app
    spec:
      containers:
        - name: application
          image: forbsey/go-web-application
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 3000
EOF
```

<br/>

    $ kubectl get deployments
    NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
    go-web-application   3/3     3            3           32s

<br/>


<br/>


```yaml
$ cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
  name: go-web-service
spec:
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 3000
  selector:
    name: go-web-app
EOF
```

<br/>

    $ kubectl get svc
    NAME             TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
    go-web-service   LoadBalancer   10.245.5.207   157.245.25.92   80:31696/TCP   2m49s
    kubernetes       ClusterIP      10.245.0.1     <none>          443/TCP        22m


<br/>


http://157.245.25.92