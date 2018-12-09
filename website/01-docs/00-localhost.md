---
layout: page
title: Развернуть локально у себя
permalink: /localhost/
---

<br/>

# Развернуть локально у себя


**Инсталляция ПО:**

Необходим установленный ruby on rails (Также как в уроках от otus devops).

Ссылка на репо внизу:

    gem install jekyll

(Вроде достаточно get install)

<br/>

**Для запуска:**

    jekyll serve --watch --host 0.0.0.0 --port 8080

Или

    JEKYLL_ENV=production bundle exec jekyll serve --host 0.0.0.0 --port 8080