---
layout: page
title: Запустить Node.js + React + MongoDB одной командой
description: Запустить Node.js + React + MongoDB одной командой
permalink: /devpos/docker/node-react-mongo/
---

<br/>

# Запустить Node.js + React + MongoDB одной командой

**Само приложение:**

https://github.com/webmakaka/learning-full-stack-javascript-development-mongodb-node-and-react

<br/>

**Команда для запуска:**

```
$ docker run -it \
-p 80:8080 \
--name learning-full-stack-javascript-development-mongodb-node-and-react \
marley/learning-full-stack-javascript-development-mongodb-node-and-react
```

<br/>

http://localhost/

<br/>

    // Удалить потом контейнер можно командой
    $ docker rm learning-full-stack-javascript-development-mongodb-node-and-react
