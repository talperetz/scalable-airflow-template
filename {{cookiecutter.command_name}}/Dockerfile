FROM python:3.7-slim-buster

ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

ARG APP_HOME=/usr/local/app/

COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . $APP_HOME

RUN chown -R app: ${APP_HOME}
USER app
WORKDIR ${APP_HOME}
ENTRYPOINT ["/entrypoint.sh"]
CMD ["webserver"]