# Pull base image.
FROM dockerfile/ubuntu

# Install Haproxy.
RUN \
  sed -i 's/^# \(.*-backports\s\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get install -y haproxy=1.5.3-1~ubuntu14.04.1 && \
  sed -i 's/^ENABLED=.*/ENABLED=1/' /etc/default/haproxy && \
  rm -rf /var/lib/apt/lists/*

# Define working directory.
WORKDIR /etc/haproxy

# Install confd
ADD https://github.com/kelseyhightower/confd/releases/download/v0.6.3/confd-0.6.3-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd

VOLUME /etc/confd

RUN mkdir -p /etc/confd/{conf.d,templates}

COPY ./haproxy.toml /etc/confd/conf.d/haproxy.toml
COPY ./haproxy.tmpl /etc/confd/templates/haproxy.tmpl
COPY ./confd-watch /usr/local/bin/confd-watch
RUN chmod +x /usr/local/bin/confd-watch

# Expose ports.
EXPOSE 80
EXPOSE 443

CMD ["/usr/local/bin/confd-watch"]