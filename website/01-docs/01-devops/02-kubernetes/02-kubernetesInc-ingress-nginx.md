---
layout: page
title: KubernetesInc Ingress Nginx
permalink: /linux/servers/containers/kubernetes/kubeadm/ingress/kubernetesinc-ingress-nginx/
---

# KubernetesInc Ingress Nginx

Делаю  
24.04.2019

# Пример из видеокурса Learn DevOps The Complete Kubernetes Course

Кластер подготовлен как <a href="/linux/servers/containers/kubernetes/single-master/">здесь</a>.

<br/>

    В общем, если использовать последнюю версию ingress controller (mandatory.yaml), что предлагают на github, то не работает. Я по быстрому не разобрался в чем причина. Может потом, когда будет более актуально. Также выслушаю предложения в чате.

<br/>

    $ cd ~/tmp
    $ curl -LJO https://raw.githubusercontent.com/wardviaene/kubernetes-course/master/ingress/nginx-ingress-controller.yml

    $ vi nginx-ingress-controller.yml

меняю версию nginx-ingress-controller:0.17.1 на nginx-ingress-controller:0.24.1

    $ kubectl create -f nginx-ingress-controller.yml

<!--

    // ingress controller
    $ kubectl create -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml

-->

<br/>

    $ kubectl create -f https://raw.githubusercontent.com/wardviaene/kubernetes-course/master/ingress/ingress.yml

<br/>

    $ kubectl create -f https://raw.githubusercontent.com/wardviaene/kubernetes-course/master/ingress/echoservice.yml

    $ kubectl create -f https://raw.githubusercontent.com/wardviaene/kubernetes-course/master/ingress/helloworld-v1.yml

    $ kubectl create -f https://raw.githubusercontent.com/wardviaene/kubernetes-course/master/ingress/helloworld-v2.yml

    $ kubectl get pods

    $ curl 192.168.0.11

    $ curl http://192.168.0.11 -H 'Host:helloworld-v1.example.com'
    Hello World!

<br/>

Устанавливю haproxy.

<br/>

### Далее на host машине

<br/>

    $ echo "192.168.0.5 helloworld-v1.example.com" | sudo tee -a /etc/hosts

    $ echo "192.168.0.5 helloworld-v2.example.com" | sudo tee -a /etc/hosts

<br/>

    $ curl helloworld-v1.example.com
    $ curl helloworld-v2.example.com
    OK
