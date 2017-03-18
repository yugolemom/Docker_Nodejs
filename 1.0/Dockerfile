FROM openshift/base-centos7

MAINTAINER Hugo C. Lima <yugolemom@gmail.com>

ENV NODE_VERSION 7.5.0

LABEL io.k8s.description="Nodejs - NPM" \
      io.k8s.display-name="Nodejs" \
      io.openshift.expose-services="8080:http,8888:ping" \
      io.openshift.tags="builder,nodejs" \
      io.openshift.s2i.destination="/tmp"

# Install NodeJS e NPM
RUN yum install -y --enablerepo=centosplus tar unzip bc which lsof wget curl \
    && yum clean all -y \
    && wget "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
  && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.xz" \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

COPY .s2i/bin/ $STI_SCRIPTS_PATH

USER 1001
EXPOSE 8080
