---
layout: page
title: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Контейнеры
description: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Контейнеры
keywords: Видеокурсы по DevOps, Внедрение полного конвейера CI/CD, Контейнеры
permalink: /videos/devops/implementing-a-full-ci-cd-pipeline/containers/
---

# [A Cloud Guru, Linux Academy] Внедрение полного конвейера CI/CD [RUS, 2020]

<br/>

## 06. Контейнеры

<br/>

Устанавливаю <a href="//sysadm.ru/devops/containers/docker/setup/ubuntu/">Docker</a> на хосте, на котором уже уснановлен Jenkis.

<br/>

https://github.com/linuxacademy/cicd-pipeline-train-schedule-docker/blob/example-solution/Dockerfile

<br/>

### 26. Установка Docker в Jenkins

    $ sudo usermod -aG docker jenkins
    $ sudo systemctl restart jenkins
    $ sudo systemctl restart docker

<br/>

### 27. Непрерывная доставка с Jenkins Pipelines и докеризованное приложение

<br/>

**Jenkins**

Manage Jenkins -> Configure System

Global properties

-   Environment variables

<br/>

```
Name: prod_id
Value: <IP>
```

<br/>

<br/>

**Jenkins**

Manage Jenkins -> Credentials

webserver_login
docker_hub_login

https://github.com/linuxacademy/cicd-pipeline-train-schedule-dockerdeploy

<br/>

Финальная версия Jenkinsfile из демонстрации в ветке example-solution данного проекта:

https://github.com/linuxacademy/cicd-pipeline-train-schedule-dockerdeploy/blob/example-solution/Jenkinsfile
