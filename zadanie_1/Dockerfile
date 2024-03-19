FROM ubuntu:22.04

ENV TZ="Europe/Warsaw"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update #&& apt-get upgrade -y
RUN apt-get install -y software-properties-common sudo openssl curl unzip
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update && apt-get install -y python3.8 openjdk-8-jdk kotlin
WORKDIR /root/
ADD https://services.gradle.org/distributions/gradle-8.6-bin.zip /root/
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-8.6-bin.zip
RUN ln -s /opt/gradle/gradle-8.6/bin/gradle /usr/bin/gradle

EXPOSE 9000

RUN adduser -shell /bin/bash student
RUN adduser student sudo
RUN usermod -p "$(openssl passwd -6 haslo)" student
USER student
WORKDIR /home/student/

RUN mkdir gradle_project && cd gradle_project
RUN gradle init --type kotlin-application --dsl groovy --project-name gradle_project --java-version 8 --use-defaults
RUN echo "dependencies { implementation group:'org.xerial', name:'sqlite-jdbc', version:'3.45.2.0' }" >> app/build.gradle

CMD ./gradlew run
