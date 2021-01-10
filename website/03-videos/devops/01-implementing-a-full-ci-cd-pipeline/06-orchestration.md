---
layout: page
title: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Оркестрация
description: Видеокурсы по DevOps - Внедрение полного конвейера CI/CD - Оркестрация
keywords: Видеокурсы по DevOps, Внедрение полного конвейера CI/CD, Оркестрация
permalink: /videos/devops/implementing-a-full-ci-cd-pipeline/orchestration/
---

# [A Cloud Guru, Linux Academy] Внедрение полного конвейера CI/CD [RUS, 2020]

<br/>

## 07. Оркестрация

Клонируем к себе в репо на гитхаб

https://github.com/linuxacademy/cicd-pipeline-train-schedule-kubernetes

<br/>

В Jenkins Нужно установить Plugin "Kubernetes Continuous Deploy"

<!--

<br/>

Kubernetes
Также установил Plugin "Kubernetes Client API"


-->

<br/>

Разворачиваю <a href="https://github.com/webmakaka/vagrant-kubernetes-3-node-cluster-centos7">kubernetes</a> в виртуалках.

<br/>

Jenkins -> Credentials:

github_token -> github_api_key
Docker_hub_login -> создан ранее

<br/>

Add Credentials ->

Kind -> Kubernetes configuration (kubeconfig)

id: kubeconfig
Description: Kubeconfig

Kubeconfig -> Enter directly ->

Вставляю содержимое файла

    $ cat /home/marley/.kube/config

<br/>

Jenkins -> New Item

Name: train-schedule
Type: Multibranch Pipeline

<br/>

Branch Source -> GitHub

Credentials -> Github API Key

Repository HTTPS URL

https://github.com/webmak1/cicd-pipeline-train-schedule-kubernetes

validate.

<br/>

Добавляем в проект github

https://github.com/linuxacademy/cicd-pipeline-train-schedule-kubernetes/blob/example-solution/train-schedule-kube.yml

<br/>

Заменяем Jenkinsfile и в нем docker-hub:

https://github.com/linuxacademy/cicd-pipeline-train-schedule-kubernetes/blob/example-solution/Jenkinsfile

<br/>

На шаге развертывания ошибка.

```
ERROR: ERROR: Can't construct a java object for tag:yaml.org,2002:io.kubernetes.client.openapi.models.V1Service; exception=Class not found: io.kubernetes.client.openapi.models.V1Service
 in 'reader', line 1, column 1:
    kind: Service
    ^

hudson.remoting.ProxyException: Can't construct a java object for tag:yaml.org,2002:io.kubernetes.client.openapi.models.V1Service; exception=Class not found: io.kubernetes.client.openapi.models.V1Service
 in 'reader', line 1, column 1:
    kind: Service
    ^

	at org.yaml.snakeyaml.constructor.Constructor$ConstructYamlObject.construct(Constructor.java:335)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructObjectNoCheck(BaseConstructor.java:229)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructObject(BaseConstructor.java:219)
	at io.kubernetes.client.util.Yaml$CustomConstructor.constructObject(Yaml.java:337)
	at org.yaml.snakeyaml.constructor.BaseConstructor.constructDocument(BaseConstructor.java:173)
	at org.yaml.snakeyaml.constructor.BaseConstructor.getSingleData(BaseConstructor.java:157)
	at org.yaml.snakeyaml.Yaml.loadFromReader(Yaml.java:490)
	at org.yaml.snakeyaml.Yaml.loadAs(Yaml.java:456)
	at io.kubernetes.client.util.Yaml.loadAs(Yaml.java:224)
	at io.kubernetes.client.util.Yaml.modelMapper(Yaml.java:494)
	at io.kubernetes.client.util.Yaml.loadAll(Yaml.java:272)
	at com.microsoft.jenkins.kubernetes.wrapper.KubernetesClientWrapper.apply(KubernetesClientWrapper.java:236)
	at com.microsoft.jenkins.kubernetes.command.DeploymentCommand$DeploymentTask.doCall(DeploymentCommand.java:172)
	at com.microsoft.jenkins.kubernetes.command.DeploymentCommand$DeploymentTask.call(DeploymentCommand.java:124)
	at com.microsoft.jenkins.kubernetes.command.DeploymentCommand$DeploymentTask.call(DeploymentCommand.java:106)
	at hudson.FilePath.act(FilePath.java:1164)
	at com.microsoft.jenkins.kubernetes.command.DeploymentCommand.execute(DeploymentCommand.java:68)
	at com.microsoft.jenkins.kubernetes.command.DeploymentCommand.execute(DeploymentCommand.java:45)
	at com.microsoft.jenkins.azurecommons.command.CommandService.runCommand(CommandService.java:88)
	at com.microsoft.jenkins.azurecommons.command.CommandService.execute(CommandService.java:96)
	at com.microsoft.jenkins.azurecommons.command.CommandService.executeCommands(CommandService.java:75)
	at com.microsoft.jenkins.azurecommons.command.BaseCommandContext.executeCommands(BaseCommandContext.java:77)
	at com.microsoft.jenkins.kubernetes.KubernetesDeploy.perform(KubernetesDeploy.java:42)
	at com.microsoft.jenkins.azurecommons.command.SimpleBuildStepExecution.run(SimpleBuildStepExecution.java:54)
	at com.microsoft.jenkins.azurecommons.command.SimpleBuildStepExecution.run(SimpleBuildStepExecution.java:35)
	at org.jenkinsci.plugins.workflow.steps.SynchronousNonBlockingStepExecution.lambda$start$0(SynchronousNonBlockingStepExecution.java:47)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: hudson.remoting.ProxyException: org.yaml.snakeyaml.error.YAMLException: Class not found: io.kubernetes.client.openapi.models.V1Service
	at org.yaml.snakeyaml.constructor.Constructor.getClassForNode(Constructor.java:664)
	at org.yaml.snakeyaml.constructor.Constructor$ConstructYamlObject.getConstructor(Constructor.java:322)
	at org.yaml.snakeyaml.constructor.Constructor$ConstructYamlObject.construct(Constructor.java:331)
	... 30 more
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline

Could not update commit status, please check if your scan credentials belong to a member of the organization or a collaborator of the repository and repo:status scope is selected


GitHub has been notified of this commit’s build result

ERROR: Kubernetes deployment ended with HasError
Finished: FAILURE
```

<br/>

192.168.0.11:8080

<!--
<br/>

Downgrade

https://www.youtube.com/watch?v=d6BU8LBc9Ow

Jackson 2 API to v2.10.3
Snakeyaml API to v1.26.2
github-branch-source 2.7.1

kubernetes client api 4.9.1-1

Скачиваю:

Jenkins -> Plugins -> Advanced -> Upload

https://plugins.jenkins.io/ -->
