---
layout: page
title: Single Master Kubernetes Cluster в виртуальных машинах (vagrant, kubeadm, cubectl)
permalink: /linux/servers/containers/kubernetes/kubeadm/single-master/
---

# Single Master Kubernetes Cluster в виртуальных машинах (vagrant, kubeadm, cubectl)

Делаю  
29.03.2019

Нужно поднять 3 виртуальные машины:

<br/>

    192.168.0.10 master.k8s
    192.168.0.11 node1.k8s
    192.168.0.12 node2.k8s

<br/>

    $ mkdir ~/vagrant-kubernetes && cd ~/vagrant-kubernetes

<br/>

    $ vagrant plugin install vagrant-hostmanager

<br/>

    $ git clone https://github.com/marley-js/vagrant-kuberntes.git .
    $ cd centos7

<br/>

    $ vagrant box update
    $ vagrant up

<br/>

    $ vagrant status

    master.k8s running (virtualbox)
    node1.k8s running (virtualbox)
    node2.k8s running (virtualbox)

<br/>

### Конфигурирование ведущего узла с помощью kubeadm (master.k8s)

    $ vagrant ssh master.k8s

    $ sudo su -

    // Явно указываю интерфейс к которому должны будут подключаться узлы.
    # kubeadm init --apiserver-advertise-address 192.168.0.10 --pod-network-cidr=10.244.0.0/16

<br/>

    - apiserver-advertise-address - ip сетевого интерфейса master.k8s к которому должны будут подключаться узлы.
    - pod-network-cidr - какая-то херня, чтобы заработал flanne. Нужно, чтобы контейнеры могли взаимодействовать между собой (если я все правильно понял). Network менять не нужно. Оставить как есть.

<br/>

    // Последние строки в конце скрипта. Их лучше сразу выполнить на добавляемых узлах:

    kubeadm join 192.168.0.10:6443 --token 9v3cmm.7z7r0x2gxwd3kh6g \
    --discovery-token-ca-cert-hash sha256:fb33f100fe8f626a00b65fd8411d2921ac1fff834f3f2c4669305ade67dab74f

<br/>

### Настройка рабочих узлов с помощью kubeadm (node1.k8s, node2.k8s)

    $ vagrant ssh node1.k8s

И сразу:

    $ vagrant ssh node2.k8s

На всех узлах:

    $ sudo su -

Собственно выполняем скрипт, который предлагали на master.k8s

    # kubeadm join 192.168.0.10:6443 --token 9v3cmm.7z7r0x2gxwd3kh6g \
    --discovery-token-ca-cert-hash sha256:fb33f100fe8f626a00b65fd8411d2921ac1fff834f3f2c4669305ade67dab74f

<br/>

### Настройка контейнерной сети (Развертывание плагина Flannel) (master.k8s)

    # export KUBECONFIG=/etc/kubernetes/admin.conf

<br/>

    # kubectl get nodes
    NAME         STATUS     ROLES    AGE   VERSION
    master.k8s   NotReady   master   37s   v1.14.0
    node1.k8s    NotReady   <none>   13s   v1.14.0
    node2.k8s    NotReady   <none>   12s   v1.14.0

<br/>

**Flannel**

Вариант с Weave Net у меня не заработал, но отлично заработал вариант с Flannel.

Узлы уже должны быть подключены к master.k8s.

    # kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/a70459be0084506e4ec919aa1c114638878db11b/Documentation/kube-flannel.yml

<br/>

Ждемс...Пока не будет...

    # kubectl get nodes
    NAME         STATUS   ROLES    AGE   VERSION
    master.k8s   Ready    master   89s   v1.14.0
    node1.k8s    Ready    <none>   65s   v1.14.0
    node2.k8s    Ready    <none>   64s   v1.14.0

<br/>

    # kubectl get po -n kube-system
    NAME                                 READY   STATUS    RESTARTS   AGE
    coredns-fb8b8dccf-9z7b8              1/1     Running   0          87s
    coredns-fb8b8dccf-tsxp9              1/1     Running   0          87s
    etcd-master.k8s                      1/1     Running   0          34s
    kube-apiserver-master.k8s            1/1     Running   0          35s
    kube-controller-manager-master.k8s   1/1     Running   0          45s
    kube-flannel-ds-amd64-2tx79          1/1     Running   0          47s
    kube-flannel-ds-amd64-n9v9f          1/1     Running   0          47s
    kube-flannel-ds-amd64-zqtz8          1/1     Running   0          47s
    kube-proxy-mhwpk                     1/1     Running   0          83s
    kube-proxy-w4snq                     1/1     Running   0          82s
    kube-proxy-wqrjd                     1/1     Running   0          87s
    kube-scheduler-master.k8s            1/1     Running   0          33s

<br/>

### Запуск приложения в созданном кластере

<br/>

    # mkdir ~/nodejs-cats-app && cd ~/nodejs-cats-app

<br/>

    # vi nodejs-cats-app-replicaset.yaml

```
apiVersion: apps/v1beta2
kind: ReplicaSet
metadata:
  name: nodejs-cats-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nodejs-cats-app
  template:
    metadata:
      labels:
        app: nodejs-cats-app
    spec:
      containers:
      - name: nodejs-cats-app
        image: marley/nodejs-cats-app
```

    # kubectl create -f nodejs-cats-app-replicaset.yaml

<br/>

    # vi nodejs-cats-app-svc-nodeport.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: nodejs-cats-app-nodeport
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 8080
    nodePort: 30123
  selector:
    app: nodejs-cats-app
```

    # kubectl create -f nodejs-cats-app-svc-nodeport.yaml

<br/>

    # kubectl get pods
    NAME                    READY   STATUS    RESTARTS   AGE
    nodejs-cats-app-9hldb   1/1     Running   0          12m
    nodejs-cats-app-xtr2f   1/1     Running   0          12m
    nodejs-cats-app-zhzxn   1/1     Running   0          12m

<br/>

    # kubectl get svc
    NAME                       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
    kubernetes                 ClusterIP   10.96.0.1       <none>        443/TCP        15m
    nodejs-cats-app-nodeport   NodePort    10.103.166.95   <none>        80:30123/TCP   8m41s

<br/>

Приложение запустилось. Можно подключиться:

http://192.168.0.11:30123/

http://192.168.0.12:30123/

<br/>

![cats-kubernetes](/img/cats-kubernetes.png "cats-kubernetes"){: .center-image }

<br/>

Как сделать, чтобы обращаться к какому-то определенному ip на порт 80, чтобы kubernetes сам выбирал на какой узел ему перебрасывать запрос?

Ingress у меня не заработал.
