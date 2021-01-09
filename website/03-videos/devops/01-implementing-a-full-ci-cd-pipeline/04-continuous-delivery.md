---
layout: page
title: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Непрерывная доставка
description: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Непрерывная доставка
keywords: Видеокурсы по DevOps, Внедрение полного конвейера CI/CD, Непрерывная доставка
permalink: /videos/devops/implementing-a-full-ci-cd-pipeline/continuous-delivery/
---

# [A Cloud Guru, Linux Academy] Внедрение полного конвейера CI/CD [RUS, 2020]

<br/>

## 05. Непрерывная доставка

<br/>

### 20. Развертывание с Jenkins Pipelines - Часть 1

https://github.com/linuxacademy/cicd-pipeline-train-schedule-cd

Пользователь deploy

systemctl

===================

**Jenkins**

Manage Jenkins -> Manage Plugins -> Available

-   Publish Over SSH

<br/>

**Jenkins**

Manage Jenkins -> Configure System

Publish over SSH

SSH Servers -> Add

Server1

```


Name: staging
Nostname: ip

Username:
Remote Directory: /
```

Server2

```
Name: production
Nostname: ip

Username:
Remote Directory: /
```

<br/>

Jenkins -> Credentials

Jenkins

Global credentials -> Add Credentials

Username: deploy
Password: deploy
ID: webserver_login
Description: Webserver Login

OK

<br/>

Jenkins -> New Item

Name: train-schedule
Multibranch Pipeline

Branch Sources -> Github -> Add Jenkins

Kind: Username with password

Username: GithubUserName
Password: GithubAPIKey
ID: github_api_key
Description: GitHub API Key

Add

<br/>

Gredentials: GitHub API Key
Owner: GithubUsername
Repostitory: cicd-pipeline-train-schedule-cd

Save

На этом шаге только сборка. Нет доставки.

<br/>

### 20. Развертывание с Jenkins Pipelines - Часть 2

<br/>

Заменить содержимое Jenkinsfile на

https://github.com/linuxacademy/cicd-pipeline-train-schedule-cd/blob/example-solution/Jenkinsfile
