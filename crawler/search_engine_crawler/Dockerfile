FROM python:3.8-slim
LABEL version="1.0"
ENV APP_RUNTIME /app_runtime
ENV APP_HOME /app
WORKDIR $APP_RUNTIME
COPY requirements.txt $APP_RUNTIME/

RUN pip install -r $APP_RUNTIME/requirements.txt

COPY . $APP_HOME
WORKDIR $APP_HOME

ENV MONGO mongodb
ENV MONGO_PORT 27017
ENV RMQ_HOST rabbitmq
ENV RMQ_QUEUE crawler
ENV RMQ_USERNAME guest
ENV RMQ_PASSWORD guest
ENV CHECK_INTERVAL 30
ENV URL https://vitkhab.github.io/search_engine_test_site/
ENV EXCLUDE_URLS '.*github.com'

CMD ["python3", "-u", "crawler/crawler.py" ]