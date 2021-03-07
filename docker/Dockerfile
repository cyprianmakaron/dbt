ARG BASE_IMAGE="python:3.8-slim-buster"
FROM $BASE_IMAGE

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    git \
    software-properties-common \
    make \
    build-essential \
    ca-certificates \
    libpq-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /var/cache/* /var/log/* /tmp/* /var/tmp/*

ARG BASE_REQUIREMENTS_SRC_PATH

RUN echo BASE_REQUIREMENTS_SRC_PATH=$BASE_REQUIREMENTS_SRC_PATH \
    && echo WHEEL_REQUIREMENTS_SRC_PATH=$WHEEL_REQUIREMENTS_SRC_PATH \
    && echo DIST_PATH=$DIST_PATH

ENV PYTHONUNBUFFERED=1 PYTHONIOENCODING=utf-8 LANG=C.UTF-8

RUN pip install --no-cache-dir --upgrade pip setuptools

COPY $BASE_REQUIREMENTS_SRC_PATH /requirements.txt
RUN pip install --no-cache-dir --requirement /requirements.txt

ARG DIST_PATH
ARG WHEEL_REQUIREMENTS_SRC_PATH
COPY $WHEEL_REQUIREMENTS_SRC_PATH /wheel_requirements.txt
COPY $DIST_PATH /dist
RUN pip install --no-cache-dir --requirement /wheel_requirements.txt

WORKDIR /usr/app
VOLUME /usr/app

ENTRYPOINT ["dbt"]
