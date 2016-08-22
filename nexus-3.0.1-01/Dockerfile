FROM ubuntu:14.04
MAINTAINER Zhenwei Liu <zwliu@thoughtworks.com>

ENV basedir /nexus
ENV nexus_domain nexus
ENV nexus_ip 192.168.33.31

RUN apt-get update && apt-get install software-properties-common python-software-properties -y && add-apt-repository ppa:openjdk-r/ppa -y && apt-get update &&\
apt-get install openjdk-8-jdk -y 

RUN mkdir -p ${basedir}/data/tmp

ADD nexus-3.0.1-01-unix.tar.gz /nexus/

WORKDIR ${basedir}/nexus-3.0.1-01

RUN mkdir etc/ssl
RUN cd etc/ssl && keytool -genkeypair -keystore keystore.jks -storepass nexus3 -keypass nexus3 -alias jetty -keyalg RSA -keysize 2048 -validity 5000 -dname "CN=*.${nexus_domain}, OU=Example, O=Sonatype, L=Unspecified, ST=Unspecified, C=US" -ext "SAN=DNS:${nexus_domain},IP:${nexus_ip}" -ext "BC=ca:true"

RUN sed  -i 's|\(^nexus-args=.*\)|\1,${karaf.etc}/jetty-https.xml\napplication-port-ssl=8443|' etc/org.sonatype.nexus.cfg

RUN sed -i -e 's|\(<Set name="KeyStorePassword">\).*\(</Set>\)$|\1nexus3\2|' -e 's|\(<Set name="KeyManagerPassword">\).*\(</Set>\)|\1nexus3\2|' -e 's|\(<Set name="TrustStorePassword">\).*\(</Set>\)|\1nexus3\2|' etc/jetty-https.xml

RUN sed -i -e 's|-Dkaraf.data=data|-Dkaraf.data=${basedir}/data|' -e 's|-Djava.io.tmpdir=data/tmp|-Djava.io.tmpdir=${basedir}/data/tmp|' ./bin/nexus.vmoptions

VOLUME ${basedir}/data

EXPOSE 8081
EXPOSE 8443
EXPOSE 5000

CMD ./bin/nexus run

 
