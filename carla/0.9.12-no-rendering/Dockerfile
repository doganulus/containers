FROM ubuntu:focal

ARG CARLA_RELEASE=0.9.12

EXPOSE 2000-2002

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
        sudo \
        wget \
        libomp-dev \
        libpng-dev \ 
        libtiff5-dev \
        libjpeg-dev \
        python3-dev \
        python3-pip \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN groupadd work -g 1000 \
    && useradd -ms /bin/bash carla -g 1000 -u 1000 \
    && printf "carla:carla" | chpasswd \
    && printf "carla ALL= NOPASSWD: ALL\\n" >> /etc/sudoers
    
USER carla
WORKDIR /home/carla/

RUN wget -q https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/CARLA_${CARLA_RELEASE}.tar.gz
RUN mkdir -p /home/carla/carla-simulator && tar -zxf CARLA_${CARLA_RELEASE}.tar.gz -C /home/carla/carla-simulator
RUN cd /home/carla/carla-simulator && sh ./ImportAssets.sh
RUN rm CARLA_${CARLA_RELEASE}.tar.gz

# Add a null config file to prevent missing sound card error   
# COPY asound.conf /etc/asound.conf 

# Disable rendering totally by nullrhi flag
ENTRYPOINT /home/carla/carla-simulator/CarlaUE4.sh -nullrhi 

