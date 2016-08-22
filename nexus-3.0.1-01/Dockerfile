FROM ubuntu:14.04
MAINTAINER Zhenwei Liu <zwliu@thoughtworks.com>

ENV basedir /nexus

RUN apt-get update && apt-get install software-properties-common python-software-properties -y && add-apt-repository ppa:openjdk-r/ppa -y && apt-get update &&\
apt-get install openjdk-8-jdk -y 

RUN mkdir -p ${basedir}/data/tmp

ADD nexus-3.0.1-01-unix.tar.gz /nexus/

WORKDIR ${basedir}/nexus-3.0.1-01

RUN sed -i -e 's|-Dkaraf.data=data|-Dkaraf.data=${basedir}/data|' -e 's|-Djava.io.tmpdir=data/tmp|-Djava.io.tmpdir=${basedir}/data/tmp|' ./bin/nexus.vmoptions

VOLUME ${basedir}/data

EXPOSE 8081

CMD ./bin/nexus run

 
