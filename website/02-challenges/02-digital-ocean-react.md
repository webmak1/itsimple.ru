---
layout: page
title: DEVOPS Challenges - Развернуть React (JavaScript) приложение в облаке Digital Ocean
description: Задача - Развернуть самое простое React (JavaScript) приложиение в облаке Digital Ocean
keywords: devops, challenge, react, docker, kubernetes, digital ocean
permalink: /challenges/digital-ocean-react/
---

# [DEVOPS Challenges] Challenge 1 - Развернуть React (JavaScript) приложение в облаке Digital Ocean

**Задача:**  

Развернуть самое простое <a href="https://github.com/marley-nodejs/React-hooks-writing-real-project">React (JavaScript) приложиение</a> в облаке Digital Ocean. Приложение не работает с базой данных, поэтому его можно считать простым. 

<br/>

**Шаг: 1 (Задание для devops, который хочет зарабатывать 30 000 руб.)**  
Приложение завернуть в docker контейнер и разместить в registry. Использовать какой-нибудь инструмент CI/CD. Jenkins, GitLab-CI, Github-Actions.

UPD.  
Если кто сам не хочет разбираться, вот здесь работающий пример.

https://github.com/marley-nodejs/The-React-Practice-Course-Learn-by-Building-Projects/tree/master/project1

Можно сделать по аналогии.

<br/>

**Шаг: 2 (Задание для devops, который хочет зарабатывать 40 000 руб.)**  
Поднять с помощью Terraform окружение стандартное для запуска приложения в docker контейнере. Либо поднять kubernetes (предпочтительнее).

<br/>

**Шаг: 3 (Задание для devops, который хочет зарабатывать 50 000 руб.)**  
Развернуть приложение. Предоставить доспут к приложению по http.

<br/>

**Шаг: 4 (Необязательный) (Задание для devops, который хочет зарабатывать 60 000 руб.)**  
Добавить домен для обращения к приложению по имени

<br/>

**Шаг: 5 (Необязательный) (Задание для devops, который хочет зарабатывать 70 000 руб.)**  
Сделать доступ только по https. (Без использования всяких cloudflare и им подобным сервисам.)

<br/>

**Шаг: 6 (Необязательный) (Задание для devops, который хочет зарабатывать 80 000 руб.)**  
Автообновление приложения после каждого коммита. Или по расписанию.


<br/>

### Обсуждение в телеграм группе

(Если кто придет из интернетов)

https://t.me/otus_devops

<br/>

### Полезные материалы

**Промо на $ 100 от Digital Ocean**  
https://pages.news.digitalocean.com/n/VBIy200V3j0D300E6GyQvX0

<br/>

**И вот здесь тоже давали $100**  
do.co/mason



<br/>

### [Webinar] Using Infrastructure as Code to Build Reproducible Systems with Terraform on DigitalOcean

(Если появится на youtube, добавлю)

https://github.com/Zelgius/Infrastructure-As-Code-Intro

<br/>

Вот это, наверное лучше.

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/videoseries?list=PLtK75qxsQaMIHQOaDd0Zl_jOuu1m3vcWO" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

https://github.com/groovemonkey/digitalocean-terraform


<br/>

### [Webinar] A DigitalOcean Workshop: Get Started with Containers and Kubernetes

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/7WOgYfZgSf0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

### Кому нужны бесплатные домены

Могут из взять на сайте freenom.com

<br/>

### Кому интересно и хочет поучаствовать

Делайте форк проекта к себе.  
Работаете со своей версией проекта. Использовать свой registry (например, hub.docker.com)

В проект добавить Dockerfile, а также скрипты terraform (У меня пока поверхностные знания о terraform) и другие скрипты, если требуются. 

В Readme.md добавить информацию как запускать.

<br/>

### Посмотреть проекты участников

<a href="https://github.com/marley-nodejs/React-hooks-writing-real-project/network/members">Здесь</a>.


Все самое лучшее из наработок (если такие конечно будут), потом включу в этот проект.