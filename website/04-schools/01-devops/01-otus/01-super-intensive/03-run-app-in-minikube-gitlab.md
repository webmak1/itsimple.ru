---
layout: page
title: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
description: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
keywords: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
permalink: /schools/devops/otus/super-intensive/run-app-in-minikube-gitlab/
---

# 03. Запуск приложения в MiniKube с помощью GitLab

<br/>

    $ cat ~/.kube/config | base64

<br/>

GitLab -> Project -> Settings -> CI/CD -> Variables

<br/>

Variables - не Protected

<br/>

KUBE_CONFIG -> результат выполнения cat.

```
stages:
...
- deploy



deploy:
stage: deploy
script:
- apk add -U openssl curl tar gzip bash ca-certificates git
- curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s
https://storage.googleapis.com/kubernetes-
release/release/stable.txt)/bin/linux/amd64/kubectl
- chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl
- mkdir -p ~/.kube/ && echo $KUBE_CONFIG | base64 -d > ~/.kube/config
- kubectl cluster-info
- kubectl apply -f kubernetes/
```

<br/>

### 07 - deploy

```
deploy:
stage: deploy
script:
- apk add -U openssl curl tar gzip bash ca-certificates git


- curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s
https://storage.googleapis.com/kubernetes-
release/release/stable.txt)/bin/linux/amd64/kubectl
- chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl
- mkdir -p ~/.kube/ && echo $KUBE_CONFIG | base64 -d > ~/.kube/config
- kubectl cluster-info
- curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
| bash
- helm upgrade ui -i chart/
```
