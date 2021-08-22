FROM ubuntu:bionic
ARG LSB_RELEASE=bionic
ARG CARLA_RELEASE=0.9.11

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        gnupg2 \
        software-properties-common \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

# Setup the Debian repository
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1AF1527DE64CB8D9
RUN add-apt-repository "deb [arch=amd64] http://dist.carla.org/carla ${LSB_RELEASE} main"

# Install CARLA
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        carla-simulator=${CARLA_RELEASE} \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 
    
EXPOSE 2000-2002    

# Add a null config file to prevent missing sound card error   
COPY asound.conf /etc/asound.conf 

# Disable rendering totally by nullrhi flag
CMD /opt/carla-simulator/CarlaUE4.sh -nullrhi 

