FROM phusion/baseimage:0.9.15

# Ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

ENV HOME /root

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# With SSH. No need because of docker exec
#CMD ["/sbin/my_init","--enable-insecure-key"]
CMD ["/sbin/my_init"]

RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -qq vim curl wget build-essential python-software-properties
RUN echo 'alias vi=vim' > /etc/bash.bashrc
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -qq --force-yes mongodb-org-shell

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
