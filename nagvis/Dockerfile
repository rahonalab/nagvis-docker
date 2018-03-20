#Rahona be Labs
# Dockerfile for an icingaweb2 system
#Contains code from
# https://github.com/jjethwa/icinga2
#and following https://github.com/Icinga/icingaweb2/blob/master/doc/20-Advanced-Topics.md#web-setup-automation

#Use debian:jessie
FROM php:apache

ENV PORT 8080

MAINTAINER Luigi - Rahona Labs

#First apt-get batch
RUN export DEBIAN_FRONTEND=noninteractive \
     && apt-get update \
     && apt-get upgrade -y \
     && apt-get install -y --no-install-recommends \
	  curl \
          gcc  \
	  gnupg2 \
	  graphviz \
          logrotate \
          mysql-client \
          net-tools \
          ntp       \
          procps \
          python \
          python-dev \
          pwgen \
	  rsync \
          tcpdump \
          sudo \
          supervisor \
          unzip \
          wget \
     && apt-get clean \
     && rm -rf /var/lib/apt/lists/*

ADD content/ /

#Get NAGVIS
RUN mkdir -p /tmp/nagvis \
    && wget -q --no-cookies -O - "https://github.com/nagvis/nagvis/archive/master.tar.gz" \
    | tar vxz --strip-components=1 --directory=/tmp/nagvis -f - nagvis-master/ \
    && cd /tmp/nagvis \
    && ./install.sh -u www-data -g www-data -w /etc/apache2/sites-available -a y -q -F

RUN mv /usr/local/nagvis /usr/local/nagvis.dist
 
# Initialize and run Supervisor
ENTRYPOINT ["/opt/run"]
