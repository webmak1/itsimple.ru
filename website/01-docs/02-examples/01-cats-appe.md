---
layout: page
title: Запустить приложение с котиками одной командой
permalink: /examples/cats-app/
---

<br/>

# Запустить приложение с котиками одной командой

**Само приложение:**

https://github.com/marley-nodejs/cats-app

<br/>

**Команда для запуска:**

docker должен быть установлен!!!

    $ docker run -it \
    -p 80:8080 \
    --name nodejs-cats-app \
    marley/nodejs-cats-app

http://localhost
