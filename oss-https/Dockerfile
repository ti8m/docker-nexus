FROM       sonatype/nexus:oss
MAINTAINER ti8m forge <forge@ti8m.ch>

# Switch to user root and modify some files
# See https://books.sonatype.com/nexus-book/reference/ssl-sect-ssl-direct.html
USER root

RUN sed -i '/wrapper.app.parameter.2/a wrapper.app.parameter.3=./conf/jetty-https.xml' /opt/sonatype/nexus/bin/jsw/conf/wrapper.conf \
 && sed -i '/application-port=/a application-port-ssl=8443' /opt/sonatype/nexus/conf/nexus.properties \
 && sed -i 's#\(<Set name="keyStore">\)\(.*\)\(</Set>\)#\1/etc/ssl/nexus/nexus-keystore.jks\3#g' /opt/sonatype/nexus/conf/jetty-https.xml \
 && sed -i 's#\(<Set name="trustStore">\)\(.*\)\(</Set>\)#\1/etc/ssl/nexus/nexus-keystore.jks\3#g' /opt/sonatype/nexus/conf/jetty-https.xml \
 && sed -i 's#\(<Set name="keyStorePassword">\)\(.*\)\(</Set>\)#\1changeit\3#g' /opt/sonatype/nexus/conf/jetty-https.xml \
 && sed -i 's#\(<Set name="keyManagerPassword">\)\(.*\)\(</Set>\)#\1changeit\3#g' /opt/sonatype/nexus/conf/jetty-https.xml \
 && sed -i 's#\(<Set name="trustStorePassword">\)\(.*\)\(</Set>\)#\1changeit\3#g' /opt/sonatype/nexus/conf/jetty-https.xml

USER nexus

ENV NEXUS-KEYSTORE /etc/ssl/nexus
ENV LAUNCHER_CONF ./conf/jetty.xml ./conf/jetty-https.xml ./conf/jetty-requestlog.xml

VOLUME ${NEXUS-KEYSTORE}
