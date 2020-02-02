---
layout: page
title: Запустить приложение с котиками одной командой
description: Запуск в docker контейнере приложения с котиками одной командой в linux 
permalink: /devpos/docker/cats-app/
---

<br/>

# Запустить приложение с котиками одной командой

**Само приложение:**

https://github.com/marley-nodejs/cats-app

<br/>

**Команда для запуска:**

docker должен быть установлен!!!

```
    $ docker run -it \
    -p 80:8080 \
    --name nodejs-cats-app \
    marley/nodejs-cats-app
```

http://localhost
