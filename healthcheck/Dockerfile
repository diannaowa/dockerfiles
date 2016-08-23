FROM ubuntu:14.04
MAINTAINER zwliu

ADD check.sh /

HEALTHCHECK --interval=5m --timeout=3s \
 CMD /check.sh

CMD top
