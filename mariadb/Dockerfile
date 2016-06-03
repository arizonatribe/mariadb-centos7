FROM arizonatribe/centos
MAINTAINER David Nunez <arizonatribe@gmail.com>

# Install mariadb and additional tools it will use
RUN yum install -y --setopt=tsflags=nodocs \
    bind-utils \
    hostname \
    mariadb-server \
    psmisc \
    pwgen

RUN yum -y clean all

# Scripts in this directory overlay the container's natural directory structure
COPY docker /

RUN /opt/bin/permissions.sh /var/lib/mysql/  \
    && /opt/bin/permissions.sh /var/log/mariadb/ \
    && /opt/bin/permissions.sh /var/run/

ENTRYPOINT ["/usr/bin/start"]

# Will run as mysql user (27)
USER 27

# A range of possible ports, choose the one you want in the `docker run`/`docker-compose.yml`
# and override the `mysqld_safe` below with `mysqld_safe --port=<my chosen port>` in your
# docker-compose.yml or `docker run ... mysqld_safe --port=<my chosen port>`
EXPOSE 3306-3356

CMD ["mysqld_safe"]
