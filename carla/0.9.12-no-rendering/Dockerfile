FROM ubuntu:focal

ARG CARLA_RELEASE=0.9.12

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        wget \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN wget -q https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/CARLA_${CARLA_RELEASE}.tar.gz
RUN tar -zxf CARLA_${CARLA_RELEASE}.tar.gz --directory /opt/carla-simulator
RUN cd /opt/carla-simulator && sh ./ImportAssets.sh
RUN rm CARLA_${CARLA_RELEASE}.tar.gz
    
EXPOSE 2000-2002    

# Add a null config file to prevent missing sound card error   
# COPY asound.conf /etc/asound.conf 

# Disable rendering totally by nullrhi flag
ENTRYPOINT /opt/carla-simulator/CarlaUE4.sh -nullrhi 


