ARG CENTOS_VERSION=7
FROM centos:${CENTOS_VERSION}
LABEL Maintainer="Liem Pham <tanliemph@gmail.com>"

# this image uses PHP 7.1 & Node.js 8.x 
RUN curl https://dl.yarnpkg.com/rpm/yarn.repo > /etc/yum.repos.d/yarn.repo && \
    curl 'https://setup.ius.io/' -o setup-ius.sh && bash setup-ius.sh && \
    curl -sL https://rpm.nodesource.com/setup_8.x | bash -

RUN yum -y install epel-release && \ 
    yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd && \
    yum -y install nodejs && \ 
    npm install pm2 -g && \
    yum -y install yarn && \
    yum -y install gcc-c++ make && \
    yum -y install mod_php71u php71u-cli php71u-common php71u-json php71u-mbstring php71u-mysqlnd && \
    curl -k -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    yum -y install git && \
    yum clean all

EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
