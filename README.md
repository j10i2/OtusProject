# Описание приложения и его архитектуры

## Использовалось готовое микросервисное приложение от Otus

https://github.com/express42/search_engine_crawler

https://github.com/express42/search_engine_ui

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


