---
layout: page
title: 06. Prometheus & Grafaran
description: 06. Prometheus & Grafaran
keywords: schools, devops, otus, super intensive, minikube, prometheus, grafana
permalink: /schools/devops/otus/super-intensive/prometheus-and-grafana/
---

# 06. Prometheus & Grafaran

### [Запуск Prometheus (мониторинг) и Grafana (визуализация) в kuberntes cluster с помощью heml](//sysadm.ru/devops/containers/kubernetes/monitoring/prometheus-and-grafana-test-only/)

<br/>

<!--

```
$ helm repo add bitnami https://charts.bitnami.com/bitnami

$ helm search repo prometheus-operator

$ helm uninstall prometheus-operator bitnami/prometheus-operator --namespace prometheus
```
-->

<br/>

Предлагается обновить HelmChart. Добавить

<br/>

```
name: http-metrics
```

<br/>

```yaml
apiVersion: v1
kind: Service
metadata:
    name: frontend
    labels:
        name: frontend
spec:
    ports:
        - protocol: 'TCP'
          name: http-metrics
          port: 80
          targetPort: 4200
    selector:
        app: frontend
```

<!--

<br/>

```yaml
kind: Service
apiVersion: v1
metadata:
  name: {{ .Chart.Name }}
  labels:
    {{- range $key, $value := .Values.labels }}
      {{ $key }}: {{ $value }}
    {{- end }}
spec:
  type: {{ .Values.service.type }}
  selector:
    {{- range $key, $value := .Values.labels }}
      {{ $key }}: {{ $value }}
    {{- end }}
  ports:
  - protocol: TCP
    name: http-metrics
    port: {{ .Values.service.port }}
    targetPort: {{ .Values.service.targetPort }}
```

-->

<!--

<br/>

И использовать

<br/>

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
    name: reddit-servicemonitor
    labels:
        release: prometheus
spec:
    namespaceSelector:
        any: true
    endpoints:
    - port: http-metrics
    jobLabel: reddit
    selector:
        matchLabels:
            app: reddit
```

-->

<br/>

```yaml

$ cat <<EOF | kubectl apply -f -
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
    name: frontend-servicemonitor
    labels:
        release: prometheus
spec:
    namespaceSelector:
        any: true
    endpoints:
    - port: http-metrics
      interval: 15s
    jobLabel: frontend
    selector:
        matchLabels:
            app: frontend
EOF
```

<br/>

```
$ kubectl get ServiceMonitor
NAME                                                 AGE
frontend-servicemonitor                              20m
```

<br/>

http://localhost:9090/config

Появился frontend-servicemonitor

И в Targets

<br/>

Конфигурация Prometheus обновляется
каждые три минуты.

Применилось ли обновление можно посмотреть командой:

```
// Не работает
$ kubectl logs prometheus-kube-prometheus-operator-8559bf778-6w4x7 prometheus-config-reloader
```

<br/>

Для визуализации предлагают применить dashboard-configmap.yaml

https://gist.githubusercontent.com/vitkhab/02af337e83e66f33903f0320938135f0/raw/73b6c177be97b89e0749bb5ed122b452da094997/reddit-dashboard-configmap.yml

Должен появиться в Grafana dashboard Reddit Monitoring
