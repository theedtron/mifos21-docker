FROM FROM ghcr.io/nirmata/tomcat9-zulu-openjdk-alpine:17.30.15-jre

USER root

RUN apk add --no-cache mysql-client curl

COPY ./server.xml /usr/local/tomcat/conf/server.xml

COPY ./setenv.sh /usr/local/tomcat/bin/setenv.sh

COPY ./fineract-provider.war /usr/local/tomcat/webapps/fineract-provider.war

COPY ./apps/community-app/ /usr/local/tomcat/webapps/ROOT

COPY ./api-docs /usr/local/tomcat/webapps/api-docs

#COPY ./test/ /usr/local/tomcat/webapps/test/

RUN mkdir -p /root/.mifosx

COPY ./pentahoReports /root/.mifosx/pentahoReports

COPY ./pentaholibs /usr/local/tomcat/webapps/WEB-INF/lib

COPY ./libs /usr/local/tomcat/lib

ADD ./entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

RUN mkdir -p /run/mysqld \
	&& chown 999 /run/mysqld

RUN ls -lrt /usr/local/tomcat/webapps/

ENTRYPOINT ["sh","/entrypoint.sh"]
