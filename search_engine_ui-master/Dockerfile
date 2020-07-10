FROM python:3
WORKDIR /app
ADD . /app
RUN pip install --upgrade pip
RUN pip install -r /app/requirements.txt
ENV MONGO_PORT 27017
ENV MONGO mongo
ENV FLASK_APP=ui.py
EXPOSE 8000
CMD ["gunicorn", "ui:app", "-b", "0.0.0.0"]