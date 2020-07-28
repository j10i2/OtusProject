FROM python:3.6-alpine
LABEL version="1.0"
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY requirements.txt $APP_HOME/
# Устанавливаем зависимости
RUN pip install -r $APP_HOME/requirements.txt
# Копирует файлы Crawler в контейнер
COPY . $APP_HOME
# Список переменных
ENV MONGO mongodb
ENV MONGO_PORT 27017
ENV RMQ_HOST rabbitmq
ENV RMQ_QUEUE crawler
ENV RMQ_USERNAME guest
ENV RMQ_PASSWORD guest
ENV CHECK_INTERVAL 30
# сайт который мы будет обрабатывать
ENV URL https://vitkhab.github.io/search_engine_test_site/
# Исключения из поиска
ENV EXCLUDE_URLS '.*github.com'
# запуск venv
ENTRYPOINT [ "./docker-entrypoint.sh" ]
CMD ["python3", "-u", "crawler/crawler.py" ]