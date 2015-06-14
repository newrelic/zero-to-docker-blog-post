# Base image setup to run all the backend services
FROM debian:wheezy
 
RUN echo "deb http://http.debian.net/debian wheezy-backports main" > /etc/apt/sources.list.d/wheezy-backports.list && \
    apt-get update && \
    apt-get install --no-install-recommends -y -t wheezy-backports ansible
 
WORKDIR /srv/service/ansible
 
COPY ansible /srv/service/ansible
COPY requirements.txt /srv/service/
 
# Run Ansible to configure the Docker image
RUN ansible-playbook service.yml
 
WORKDIR /opt/service
 
CMD ["supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
