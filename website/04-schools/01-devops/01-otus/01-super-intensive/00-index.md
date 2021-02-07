---
layout: page
title: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
description: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
keywords: Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]
permalink: /schools/devops/otus/super-intensive/
---

# Супер-интенсив "CI/CD или Непрерывная поставка с Docker и Kubernetes" [RUS, 2021]

<br/>

**Изучаемые темы:**

-   Введение в Kubernetes
-   Непрерывная поставка в Kubernetes c Helm в Gitlab
-   Интеграция Elastic и Kibana c Kubernetes (Практика не была рассмотрена).

<br/>

# Задача

Повторить изучаемый материал в локальном окружении со всеми перечисленными технологиями.

<br/>

### Обсуждение на github

https://github.com/webmak1/itsimple.ru/discussions/1

<br/>

**Итак, что мы имеем:**

<br/>

-   Исходников проектов нет. (Предлагаю использовать <a href="https://github.com/webmakaka/Packaging-Applications-with-Helm-for-Kubernetes">похожее</a>. Если кто найдет репо с оригинальными исходниками проекта, поделитесь)
-   Работа происходит на подготовленных стендах в облаках google. Планируется поднять свое окружение.

<br/>

### Инсталляция <a href="//sysadm.ru/devops/gitops/cvs/gitlab/setup/ubuntu/">GitLab</a>.

### Настройка <a href="//sysadm.ru/devops/gitops/cvs/gitlab/errors/">docker для запуска job'ов</a>.

<br/>

Клонируем приложение и пока работаем с контентом из каталога /apps/v1.

<br/>

**Kubernetes:**

<br/>

Можно обойтись minikube.

Но при желании, можно использовать скрипты для разварачивания локального kubernetes кластера, можно взять <a href="https://github.com/webmakaka/vagrant-kubernetes-3-node-cluster-ubuntu-20.04">здесь</a>.

С обычным kubernetes тоже работает. Но требуется больше ресурсов.

<br/>

### [01. Сборка и push контейнеров в registry](/schools/devops/otus/super-intensive/build-and-push/)

### [02. Запуск приложения в MiniKube с помощью Helm](/schools/devops/otus/super-intensive/run-app-in-minikube/)

### [03. Настрока хоста с GitLab для работы с MiniKube](/schools/devops/otus/super-intensive/prepare-gitlab-host-to-work-with-minikube/)

### [04. Deploy приложения с помощью GitLab и Helm в MiniKube](/schools/devops/otus/super-intensive/deploy-app-in-minikube-with-gitlab-and-helm/)

### [05. Deploy приложения с помощью GitLab и Helm в MiniKube, обновляющегося при коммите или релизе](/schools/devops/otus/super-intensive/deploy-app-in-minikube-with-gitlab-and-helm-with-updates-on-commit-or-release/)

### [06. Prometheus & Grafaran](/schools/devops/otus/super-intensive/prometheus-and-grafana/)

### [07. ELK & KIBANA]
