FROM dockerfile:haproxy

RUN cd /usr/local/bin \
  && curl -L https://github.com/kelseyhightower/confd/releases/download/v0.6.3/confd-0.6.3-linux-amd64 -o confd \
  && chmod +x confd

RUN mkdir -p /etc/confd/{conf.d,templates}

COPY ./haproxy.toml /etc/confd/conf.d/haproxy.toml
COPY ./haproxy.tmpl /etc/confd/conf.d/haproxy.tmpl
COPY ./confd-watch /usr/local/bin/confd-watch

RUN chmod +x /usr/local/bin/confd-watch

CMD ["/usr/local/bin/confd-watch"]