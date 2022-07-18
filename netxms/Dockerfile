FROM debian:bullseye
RUN apt update
RUN apt install wget lsb-release systemd -y
RUN wget http://packages.netxms.org/netxms-release-latest.deb
RUN dpkg -i netxms-release-latest.deb
RUN apt-get update
RUN apt-get install netxms-server netxms-dbdrv-pgsql -y
COPY config/netxmsd.conf /etc/netxmsd.conf
CMD [echo "createdb -O netxms netxms" | -u root psql]
CMD [echo "createuser -P netxms" | -u root psql]
CMD [echo "CREATE EXTENSION IF NOT EXISTS timescaledb CASCADE;" | -u root psql]
RUN systemctl enable netxmsd

