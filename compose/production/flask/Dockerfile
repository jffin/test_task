FROM python:3.8

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED=1

ARG USER_NAME="user"

ENV USER_NAME ${USER_NAME}
ENV CONTAINER_IMAGE_VER=v1.0.1

WORKDIR /code

RUN apt update && apt install -y gcc g++

RUN python -m pip install --upgrade pip

COPY ./requirements.txt setup.py ./
RUN python -m pip install -r requirements.txt
RUN python -m pip install -e .

COPY ./text_api text_api/
COPY ./migrations migrations/

RUN mkdir db

RUN apt purge -y gcc g++

RUN mkdir -p /home/user/nltk_data

RUN useradd ${USER_NAME} -s /sbin/nologin

RUN chown -R ${USER_NAME}:${USER_NAME} /code
RUN chown -R ${USER_NAME}:${USER_NAME} /home/user/

USER ${USER_NAME}

# it has to be run from user to save it home directory
RUN python -c "import nltk; nltk.download('punkt')"
