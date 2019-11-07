FROM nimmis/ubuntu

#Set proxy
ENV HTTP_PROXY 'http://192.168.3.20:3128'
ENV http_proxy 'http://192.168.3.20:3128'
ENV HTTPS_PROXY 'https://192.168.3.20:3128'
ENV https_proxy 'https://192.168.3.20:3128'

#Install 
RUN apt-get -y install pip

## Install Python Jason to xml plugin
RUN apt-get -y install jason2xml

ENV JAVA_HOME="/usr/orps/java/jdk1.8.0_144"
ENV PYTHON_HOME="/usr/lib/python3/"
ENV ANT_HOME="/usr/orps/apache-ant-1.9.2"
ENV PATH="${ORACLE_HOME}/bin:${JAVA_HOME}/bin:${ANT_HOME}/bin:${PYTHON_HOME}/bin::${PATH}"

RUN mkdir -p /usr/orps/java && mkdir -p /home/oracle && mkdir -p /tmp/antinstall0

ADD /var/www/test1.xml /home/oracle

RUN /bin/bash -c 'openssl base64 -in /home/oracle/test1.xml -out /home/oracle/test2.xml'

RUN /bin/bash -c 'cp /home/oracle/test2.xml /var/www/test.xml'
