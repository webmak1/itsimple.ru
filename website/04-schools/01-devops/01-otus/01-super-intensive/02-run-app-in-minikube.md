---
layout: page
title: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
description: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
keywords: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
permalink: /schools/devops/otus/super-intensive/run-app-in-minikube/
---

# 02. Запуск приложения в MiniKube

<br/>

### Docker

```
$ docker -v
Docker version 20.10.0, build 7287ab3
```

<br/>

### Minikube installation

```
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

```

<br/>

```
$ minikube version
minikube version: v1.16.0
```

<br/>

### Kubectl installation

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/

$ kubectl version --client --short
Client Version: v1.20.1

```

<br/>

### Run minikube

```
$ {
    minikube --profile devops-app config set memory 8192
    minikube --profile devops-app config set cpus 4

    // minikube --profile devops-app config set vm-driver virtualbox
    minikube --profile devops-app config set vm-driver docker

    minikube --profile devops-app config set kubernetes-version v1.20.2
    minikube start --profile devops-app
}
```

<br/>

    // Enable ingress
    $ minikube addons --profile devops-app enable ingress

<br/>

    $ minikube --profile devops-app ip
    192.168.59.2

<br/>

    $ sudo vi /etc/hosts

```
#---------------------------------------------------------------------
# Minikube
#---------------------------------------------------------------------
192.168.59.2 frontend.minikube.local
192.168.59.2 backend.minikube.local
```

<br/>

### Helm installation

    $ curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

    $ kubectl config view

    $ helm version --short
    v3.5.0+g32c2223

<br/>

### Подготовка проекта

    $ mkdir ~/projects/dev/devops/super-intensive && cd ~/projects/dev/devops/super-intensive

    $ git clone https://github.com/webmakaka/Packaging-Applications-with-Helm-for-Kubernetes .

    $ cd guestbook/charts/

    $ code .

<br/>

```
webmakaka/frontend:2.0  меняю на  webmakaka/devops-frontend:0.0.10
webmakaka/backend:2.0 меняю на  webmakaka/devops-backend:0.0.10
```

<br/>

    $ cd .../projects/dev/devops/super-intensive/apps/v1/chart

    $ helm install myguestbook guestbook

<br/>

```
$ kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
backend-6689c8d5b8-njwn8    1/1     Running   0          46s
frontend-6dd4d847bd-q257c   1/1     Running   0          46s
mongodb-746c86846c-v4wd6    1/1     Running   0          46s
```

<br/>

![Application](/img/pic-lecture02-pic01.png?raw=true)

<br/>

```
$ helm delete myguestbook
```
