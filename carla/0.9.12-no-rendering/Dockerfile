FROM ubuntu:focal
ARG CARLA_RELEASE=0.9.12

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        gnupg2 \
        software-properties-common \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

# Setup the Debian repository
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1AF1527DE64CB8D9
RUN add-apt-repository "deb [arch=amd64] http://dist.carla.org/carla focal main"

# Install CARLA
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        carla-simulator=${CARLA_RELEASE} \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

EXPOSE 2000-2002

# RUN groupadd work -g 1000 \
#    && useradd -ms /bin/bash carla -g 1000 -u 1000 \
#    && printf "carla:carla" | chpasswd \
#    && printf "carla ALL= NOPASSWD: ALL\\n" >> /etc/sudoers
    
# USER carla
# WORKDIR /home/carla/

# Disable rendering totally by nullrhi flag -nullrhi
# ENTRYPOINT /opt/carla-simulator/CarlaUE4.sh

