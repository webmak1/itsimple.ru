---
layout: page
title: Запустить приложение с котиками одной командой
permalink: /voting-game/
---

<br/>

# Запустить приложение с котиками одной командой

**Само приложение:**

https://github.com/marley-nodejs/voting-game

<br/>

**Команда для запуска:**

docker должен быть установлен!!!

    $ docker run -it \
    -p 80:8080 \
    --name nodejs-voting-game \
    marley/nodejs-voting-game