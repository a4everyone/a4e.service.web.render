FROM alpine:3.6

ARG A4E_USER=a4e
ARG A4E_USER_HOME=/home/${A4E_USER}

ENV A4E_USER=${A4E_USER}
ENV A4E_USER_HOME=${A4E_USER_HOME}
# ENV LANG C.UTF-8

COPY package.json ${A4E_USER_HOME}/work/

RUN \
# USER MANAGEMENT
     addgroup -g 1001 ${A4E_USER} \
  && adduser -D -G ${A4E_USER} ${A4E_USER} \
  && mkdir -p ${A4E_USER_HOME}/logs \
  && mkdir -p ${A4E_USER_HOME}/work \
  && mkdir -p /website/ \
  && chown -R ${A4E_USER}:${A4E_USER} ${A4E_USER_HOME} /website/ \

# INSTALLS
 && apk add --no-cache git nodejs nodejs-npm

USER ${A4E_USER}

RUN cd ${A4E_USER_HOME}/work \
  && npm install --production

USER root
RUN apk del --purge git nodejs-npm
# && curl -sL https://deb.nodesource.com/setup_6.x | bash \
# && apt-get install -y nodejs \

# CLEANUP
# && apk remove -y --purge --auto-remove curl \
# && rm -rf /home/temp \
# && rm -rf /var/lib/apt/lists/* \
# && apt-get clean

# docker run -it --rm --user a4e -v /home/pato/a4e/a4e.service.web.render/image.base/:/home/a4e/work1 -v /home/pato/a4e/a4e.service.web/website/src:/website/main/ -v /home/pato/a4e/a4e.module.web.frequent/src:/website/freq/ -v /home/pato/a4e/a4e.service.web/website/build/dev/:/website-out a4everyone/web.render:base-0.0.1-SNAPSHOT_local_master
