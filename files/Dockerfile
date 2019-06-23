FROM nginx:1.15

ENV CT_VERSION=0.19.5
ENV CT_URL=https://releases.hashicorp.com/consul-template/${CT_VERSION}/consul-template_${CT_VERSION}_linux_amd64.zip

ENV MTAIL_VERSION=v3.0.0-rc29
ENV MTAIL_URL=https://github.com/google/mtail/releases/download/${MTAIL_VERSION}/mtail_${MTAIL_VERSION}_linux_amd64

# Install required packages
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update -qq && \
    apt-get install -y curl runit unzip && \
    rm -rf /var/lib/apt/lists/*

# Install consul-template
RUN curl -o consul-template.zip -L $CT_URL && unzip consul-template.zip && rm consul-template.zip && \
    mv consul-template /usr/local/bin/consul-template

# Intasll mtail
RUN curl -o /usr/local/bin/mtail -L $MTAIL_URL && chmod +x /usr/local/bin/mtail

RUN rm -v /etc/nginx/conf.d/*

COPY nginx.conf    /etc/nginx/nginx.conf

EXPOSE 80 443 3093

CMD ["/usr/bin/runsvdir", "/etc/service"]
