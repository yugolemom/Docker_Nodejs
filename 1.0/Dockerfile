FROM openshift/base-centos7

MAINTAINER Hugo C. Lima <yugolemom@gmail.com>

ENV NODE_VERSION 7.5.0
ENV NPM_VERSION 1.4.12

LABEL io.k8s.description="Nodejs - NPM" \
      io.k8s.display-name="Nodejs" \
      io.openshift.expose-services="8080:http,8888:ping" \
      io.openshift.tags="builder,nodejs" \
      io.openshift.s2i.destination="/tmp"

# Install NodeJS e NPM
RUN yum install -y --enablerepo=centosplus \
    tar unzip bc which lsof && \
    yum clean all -y && \
    curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
  && grep " node-v$NODE_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs \
  && curl -SLO "https://nodejs.org/dist/npm/npm-$NPM_VERSION.tgz" \
  && mkdir -p /opt/npm \
  && tar -xzxf "npm-$NPM_VERSION.tgz" -C /opt/npm --strip-components=1 \
  && ln -s /opt/npm/bin/npm /usr/local/bin/npm \
  && rm npm-$NPM_VERSION.tgz

COPY .s2i/bin/ $STI_SCRIPTS_PATH

USER 1001
EXPOSE 8080
