FROM centos:7
RUN curl http://downloads.opennebula.org/repo/repo.key -o repo.key
RUN rpm --import repo.key
RUN yum-config-manager --add-repo http://downloads.opennebula.org/repo/5.4/CentOS/7/x86_64
RUN yum -y install epel-release redhat-lsb-core nmap
RUN yum -y install opennebula-sunstone
RUN /usr/share/one/install_gems --yes
RUN gem install puma
RUN mkdir /var/lib/one/.one
RUN echo "serveradmin:testtesttest" > /var/lib/one/.one/sunstone_auth
COPY sunstone-server.j2 /etc/one/sunstone-server.conf
COPY docker-entrypoint.sh ./docker-entrypoint.sh
RUN chmod +x docker-entrypoint.sh
EXPOSE 9869
ENTRYPOINT ["./docker-entrypoint.sh"]