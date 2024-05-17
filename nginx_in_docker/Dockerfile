FROM httpd

RUN apt-get update && \
    apt-get install -y \
    iputils-ping
RUN apt-get install iproute2 -y
RUN apt-get install curl -y
RUN apt-get install telnet -y
RUN apt-get install dnsutils -y
RUN apt-get install vim -y