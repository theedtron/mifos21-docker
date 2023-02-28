FROM 9.0.72-jdk11-temurin-jammy:latest

# Update GPG keys for MySQL repository
RUN  apt-key adv --keyserver keys.gnupg.net --recv-keys 8C718D3B5072E1F5

# Update GPG keys for Debian repository
RUN apt-key adv --keyserver keys.gnupg.net --recv-keys 648ACFD622F3D138

# Install packages and dependencies
RUN apt-get update && apt-get install -y --force-yes mysql-client curl && rm -rf /var/lib/apt/lists/*

# Set Tomcat environment variables
ENV CATALINA_HOME=/usr/local/tomcat
ENV PATH=$CATALINA_HOME/bin:$PATH

# Copy configuration files and web applications
COPY server.xml $CATALINA_HOME/conf/
COPY setenv.sh $CATALINA_HOME/bin/
COPY fineract-provider.war $CATALINA_HOME/webapps/
COPY apps/community-app/ $CATALINA_HOME/webapps/ROOT/
COPY api-docs $CATALINA_HOME/webapps/
COPY pentahoReports /root/.mifosx/pentahoReports/
COPY pentaholibs $CATALINA_HOME/webapps/WEB-INF/lib/
COPY libs $CATALINA_HOME/lib/

# Set up entrypoint script
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Create directories and set permissions
RUN mkdir -p /root/.mifosx \
  && mkdir -p /run/mysqld \
  && chown 999 /run/mysqld \
  && chown -R 999 $CATALINA_HOME

# Start Tomcat and run entrypoint script
USER 999
WORKDIR $CATALINA_HOME
EXPOSE 8080
CMD ["catalina.sh", "run"]
ENTRYPOINT ["/entrypoint.sh"]

