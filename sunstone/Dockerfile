FROM centos:7
RUN curl http://downloads.opennebula.org/repo/repo.key -o repo.key && rpm --import repo.key \
    && yum-config-manager --add-repo http://downloads.opennebula.org/repo/5.4/CentOS/7/x86_64 \
    && yum -y install epel-release redhat-lsb-core nmap && yum -y install opennebula-sunstone
RUN /usr/share/one/install_gems --yes && gem install puma
RUN mkdir /var/lib/one/.one
COPY create-conf.sh ./create-conf.sh
COPY docker-entrypoint.sh ./docker-entrypoint.sh
RUN chmod +x docker-entrypoint.sh
EXPOSE 9869
ENTRYPOINT ["./docker-entrypoint.sh"]