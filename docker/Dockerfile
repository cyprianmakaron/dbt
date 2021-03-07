ARG BASE_IMAGE="python:3.8-slim-buster"

FROM $BASE_IMAGE
ARG BASE_REQUIREMENTS_SRC_PATH
ARG WHEEL_REQUIREMENTS_SRC_PATH
ARG DIST_PATH
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    git \
    software-properties-common \
    make \
    build-essential \
    ca-certificates \
    libpq-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo BASE_REQUIREMENTS_SRC_PATH=$BASE_REQUIREMENTS_SRC_PATH
    && echo WHEEL_REQUIREMENTS_SRC_PATH=$WHEEL_REQUIREMENTS_SRC_PATH
    && echo DIST_PATH=$DIST_PATH
COPY $BASE_REQUIREMENTS_SRC_PATH /requirements.txt
COPY $WHEEL_REQUIREMENTS_SRC_PATH /wheel_requirements.txt
COPY $DIST_PATH ./dist
RUN pip install --no-cache-dir --upgrade pip setuptools
RUN pip install --no-cache-dir --requirement /requirements.txt
RUN pip install --no-cache-dir --requirement /wheel_requirements.txt
ENV PYTHONIOENCODING=utf-8 LANG=C.UTF-8

WORKDIR /usr/app
VOLUME /usr/app

ENTRYPOINT ["dbt"]
