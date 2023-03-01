FROM mysql:latest

# Install required packages
RUN apt-get update && \
    apt-get install -y wget unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set up the database initialization scripts
RUN mkdir -p /docker-entrypoint-initdb.d 

COPY ./00-create-databases.sql /docker-entrypoint-initdb.d/00-create-databases.sql

COPY ./01-mifospltaform-tenants-first-time-install.sql /docker-entrypoint-initdb.d/01-mifospltaform-tenants-first-time-install.sql

#COPY ./02-load_sample_data.sql /docker-entrypoint-initdb.d/02-load_sample_data.sql

VOLUME /docker-entrypoint-initdb.d
