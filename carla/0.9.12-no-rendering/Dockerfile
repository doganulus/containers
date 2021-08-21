FROM ubuntu:focal

ARG CARLA_RELEASE=0.9.12

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        wget \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN wget --progress=bar:force https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/CARLA_${CARLA_RELEASE}.tar.gz
RUN tar -xf CARLA_${CARLA_RELEASE}.tar.gz -C /opt/carla-simulator
RUN cd /opt/carl-simulator && sh ./ImportAssets.sh
RUN rm CARLA_${CARLA_RELEASE}.tar.gz
    
EXPOSE 2000-2002    

# Add a null config file to prevent missing sound card error   
# COPY asound.conf /etc/asound.conf 

# Disable rendering totally by nullrhi flag
ENTRYPOINT /opt/carla-simulator/CarlaUE4.sh -nullrhi 


