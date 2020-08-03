# Описание приложения и его архитектуры

## Использовалось готовое микросервисное приложение от Otus

https://github.com/express42/search_engine_crawler

https://github.com/express42/search_engine_ui

![Приложение от Otus](https://github.com/Vdaishi/OtusProject/blob/master/Project_scheme.png)

## В качестве инструмента IaC (Infrastructure as Code) для управления конфигурацией и инфраструктурой используется terraform.

В процессе было сделано:

1. Собраны докер образы, ссылки на DockerHub

https://hub.docker.com/repository/docker/j10i2/crawler-ui

https://hub.docker.com/repository/docker/vdaishi/crawler

2. Первый вариант поднятия инфры через docker compose

3. Написаны Terrafоrm-манифесты для gcp

4. Второй вариант разворота инфры с помощью k8s

## Все, что имеет отношение к проекту хранится в Git

## Первым делом логинимся в gcp

$ gcloud auth application-default login

## Разворачиваем инфру 

1. Через docker compose

   cd docker-compose

   docker-compose build

   docker-compose up

2. Через Terrafоrm

   cd terraform

   terraform init

   terraform apply

   gcloud container clusters get-credentials awesome-k8s-cluster --zone us-central1-c --project name-of-project


NOTES:
1. Get your 'admin' user password by running:

   kubectl get secret --namespace default grfana-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster:

   grfana-grafana.default.svc.cluster.local

   Get the Grafana URL to visit by running these commands in the same shell:

     export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grfana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace default port-forward $POD_NAME 3000

3. Login with the password from step 1 and the username: admin

