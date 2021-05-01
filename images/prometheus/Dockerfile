#docker build -t prometheus:dev .
FROM prom/prometheus

ADD prometheus.yml /etc/prometheus/prometheus.yml
USER root
RUN mv /etc/prometheus/consoles/index.html.example /etc/prometheus/consoles/index.html \
  && sed -i 's/index.html.example/index.html/' /etc/prometheus/console_libraries/menu.lib