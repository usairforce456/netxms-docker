FROM debian:bullseye
RUN wget http://packages.netxms.org/netxms-release-latest.deb
RUN sudo dpkg -i netxms-release-latest.deb
RUN sudo apt-get update
RUN apt-get install netxms-server netxms-dbdrv-pgsql
WORKDIR /config
COPY netxmsd.conf /etc/netxmsd.conf
CMD [echo "createdb -O netxms netxms" | -u root psql]
CMD [echo "createuser -P netxms" | -u root psql]
CMD [echo "CREATE EXTENSION IF NOT EXISTS timescaledb CASCADE;" | -u root psql]
RUN nxdbmgr init
RUN systemctl enable netxmsd

