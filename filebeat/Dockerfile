FROM quay.io/hellofresh/hf-baseimage

# Use baseimage-docker's init system.
# That's really important to start the system services like syslog, cron and runit.
# See https://github.com/hellofresh/hf-baseimage#important
CMD ["/sbin/my_init"]

# Filebeat installation and removal of default startup script..
# Reference: https://www.elastic.co/guide/en/beats/libbeat/1.2/setup-repositories.html
RUN apt-get update && \
    apt-get install -y curl && \
    curl -L -O https://download.elastic.co/beats/filebeat/filebeat_1.2.1_amd64.deb && \
    dpkg -i filebeat_1.2.1_amd64.deb && \
    update-rc.d -f filebeat remove

# Filebeat configuration.
COPY ./config/filebeat.yml /etc/filebeat/filebeat.yml

# Service configuration for Filebeat.
RUN mkdir -p /etc/service/filebeat
COPY ./service/run /etc/service/filebeat/run


ENV LOGSFOLDER="/tmp/logstowatch/"

VOLUME [${LOGSFOLDER}]

RUN mkdir LOGSFOLDER