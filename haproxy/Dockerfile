FROM alpine:latest
MAINTAINER Bruno Simoes <brunogsimoes@gmail.com>

ENV CONSUL_TEMPLATE_VERSION=0.13.0

# Updata wget to get support for SSL
RUN apk --update add haproxy wget

# Download consul-template
RUN ( wget --no-check-certificate https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip -O /tmp/consul_template.zip && unzip /tmp/consul_template.zip && mv consul-template /usr/bin && rm -rf /tmp/* )

# Clean up APT when done
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY config/haproxy.json /tmp/haproxy.json
COPY config/haproxy.ctmpl /tmp/haproxy.ctmpl

ENTRYPOINT ["consul-template","-config=/tmp/haproxy.json"]
