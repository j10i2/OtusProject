# проект по курсу DevOps: практики и инструменты

## Описание приложения и его архитектуры

### Приложение
В данном проекте рассматривается работа и развертывание приложения от команды  OTUS.ru

https://github.com/express42/search_engine_crawler

https://github.com/express42/search_engine_ui

![Приложение от Otus](https://github.com/Vdaishi/OtusProject/blob/master/Project_scheme.png)

### Развертывание архитектуры
Для локального развертывания приложения используются контейнеры `Docker`.
Для развертывания в `GCP` используется `Kubernetes`.

### ScreenCast

https://yadi.sk/i/zrJn4VStXX1khQ

### Краткое содержание

В процессе было сделано:

1. Собраны докер образы приложения, настроен файл развертывания приложения через Docker-Compose; 
   ссылки на DockerHub:

      1. https://hub.docker.com/repository/docker/j10i2/crawler-ui

      2. https://hub.docker.com/repository/docker/vdaishi/crawler

2. Реализовано развертывание кластера `K8S` для облачного развертывания инфраструктуры;
3. Настроено развертывание приложения в `K8S` с помощью `helm`;
4. Настроен CI\CD для развертывания приложения на `Gitlab`
5. Настроено логирование контейнеров кластера с помощью `ELK` стека и `Filebeat`
6. Настроен мониторинг контейнеров кластера с помощью `Prometheus` с визуализацией в `Grafana`

## Описание проекта

Для 



## Установка приложения локально

Приложение готово к установке с помощью `Docker-compose`

1. Локально с помощью 
   ```bash
      docker-compose build

      docker-compose up
   ```
2. Через `Terrafоrm`
   1. Развертывание кластера `K8S`
      ```bash
      cd terraform

      gcloud auth application-default login

      terraform init

      terraform apply

      gcloud container clusters get-credentials awesome-k8s-cluster --zone us-central1-c --project name-of-project
      ```
   2. Развертывание Gitlab
      ```bash
      helm install gitlab ./helm/chart/gitlab-omnibus
      ```
      В рамках Gitlab реализовано: сборка, тестирование и развертывание приложения, а также удаление приложения;
   
   3. Развертывание приложения 
      ```
      helm install crawler ./helm/chart/crawler-engine
      ```
      Приложение парсит сайт и через `UI` позволяет произвести поиск фраз , которые есть на сайте. 
      Приложение использует базу данных `MongoDB` и менеджер очередей `RabbitMQ`

   4. Мониторинг приложения
      Установка мониторинга
      ```
      helm install monitoring ./helm/chart/monitoring
      ```
      
      Мониторинг получает информацию от подов и нод кластера, 
      Для работы Алертинга необходимо настроить данные в файле `./helm/chart/stable/prometheus/values.yaml` для файла `alertmanager.yml`

      Для доступа к Grafana необходимо получить расшифрованный ключ
      ```bash
         kubectl get secret --namespace default monitoring-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
      ```

   5. Логирование приложения
      Установка логирования
      
      ```bash
      helm install logging ./helm/chart/logging
      ```

      Логирование включает в себя информацию из всех подов кластера с помощью Filebeat, отсылая данные в Logstash.

   
