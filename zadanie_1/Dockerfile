FROM ubuntu:22.04

ENV TZ="Europe/Warsaw"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y software-properties-common sudo openssl
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update && apt-get install -y python3.8

RUN adduser student
RUN adduser student sudo
RUN usermod -p "$(openssl passwd -6 haslo)" student
USER student
WORKDIR /home/student/

CMD /bin/bash
