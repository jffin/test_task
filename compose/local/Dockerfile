# This is a simple Dockerfile to use while developing
# It's not suitable for production
#
# It allows you to run both flask and celery if you enabled it
# for flask: docker run --env-file=.flaskenv image flask run
# for celery: docker run --env-file=.flaskenv image celery worker -A myapi.celery_app:app
#
# note that celery will require a running broker and result backend
FROM python:3.8

RUN mkdir /code
WORKDIR /code

COPY ./requirements.txt setup.py tox.ini ./
RUN python -m pip install -r requirements.txt
RUN python -m pip install -e .

RUN python -m pip install flask_cors

RUN python -c "import nltk; nltk.download('punkt')"

COPY ./text_api text_api/
COPY ./migrations migrations/
COPY ./text_api.ini text_api.ini

EXPOSE 5000
