FROM python:3.7-alpine

ENV PYTHONUNBUFFERED 1

COPY ./requirements.txt requirements.txt

RUN pip install -r /requirements.txt

RUN apk update \
    && apk add --virtual build-deps gcc python3-dev musl-dev \
    && apk add jpeg-dev zlib-dev libjpeg \
    && pip install Pillow \
    && apk del build-deps

RUN mkdir /backend 
WORKDIR /backend

COPY ./backend /backend

RUN adduser -D user

USER user

WORKDIR /backend

CMD sh -c "python manage.py runserver 0.0.0.0:8000"