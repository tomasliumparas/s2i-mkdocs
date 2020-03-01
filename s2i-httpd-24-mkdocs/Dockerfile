FROM centos/httpd-24-centos7

ENV PATH=$HOME/.local/bin/:$PATH \
    PYTHONIOENCODING=UTF-8 \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8

EXPOSE 8080
EXPOSE 8443

USER 0

RUN yum install -y \
      python3 \
      python3-devel \
      gcc && \
    yum -y clean all --enablerepo='*'

# Drawio & dependencies
RUN yum install -y wget \
      alsa-lib && \
    wget https://github.com/jgraph/drawio-desktop/releases/download/v12.6.5/draw.io-x86_64-12.6.5.rpm -O drawio.rpm && \
    yum install -y drawio.rpm && \
    yum -y clean all --enablerepo='*'


COPY ./s2i/bin/ /usr/libexec/s2i

RUN chown -R 1001:1001 /opt/app-root

USER 1001

CMD ["/usr/bin/run-httpd"]
