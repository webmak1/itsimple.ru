---
layout: page
title: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - 02. Управление версиями исходного кода
description: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - 02. Управление версиями исходного кода
keywords: Видеокурсы по DevOps, Внедрение полного конвейера CI/CD
permalink: /videos/devops/implementing-a-full-ci-cd-pipeline/build-automation/
---

# [A Cloud Guru, Linux Academy] Внедрение полного конвейера CI/CD [RUS, 2020]

<br/>

## 03. Автоматизация сборки

<br/>

### 11. Установка Gradle

Устанавливаю <a href="//javadev.org/devtools/jdk/install/linux/">JDK8</a>

Устанавливаю <a href="//javadev.org/devtools/assembly-tools/gradle/linux/ubuntu/">Gradle</a>

<br/>

### Запуск Gradle Wrapper

    $ cd cicd-pipeline-train-schedule-git
    $ gradle wrapper

Добавить в .gitignore

```
.gradle
```

    $ ./gradlew build

<!--

<br/>

### 12. Основы Gradle

    $ gradle init

-->
