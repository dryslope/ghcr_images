FROM quay.io/centos/centos:stream9
MAINTAINER thibault.gainche@atos.net

# Sed repos to access them
#RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-*
#RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Linux-*

# Add influxdata repo
COPY ./influxdb.repo /etc/yum.repos.d/influxdb.repo

# Install development tools and other packages
RUN yum groupinstall -y "Development Tools"
RUN python3 -V
RUN yum -y install --nogpgcheck \
    expect \
    gcc \
    libffi-devel \
    make \
    postfix \
    postgresql-devel \
    #python3.8 \
    #python38-devel \
    #python38-pip \
    #python38-setuptools \
    #python38-lxml \
    libxslt-devel \
    libxml2-devel \
    rpmlint \
    libevent \
    libevent-devel \
    ncurses \
    ncurses-devel \
    rpm-build \
    telegraf

# Install tmux
COPY sources/tmux-2.9a.tar.gz ./
RUN tar -zxvf tmux-2.9a.tar.gz
RUN cd tmux-2.9a; ./configure && make; make install

# Clean up
RUN yum clean all

RUN yum install -y pip
# Upgrade pip to allow installation of backport requirement and install basic pip packages
RUN pip install --upgrade pip
RUN pip install coverage \
    mock \
    nose \
    unittest2 \
    pycodestyle \
    pylint \
    Sphinx \
    sphinx_rtd_theme \
    sphinx-prompt \
    sphinxcontrib-httpdomain \
    Sphinx-Substitution-Extensions \
    argparse \
    requests \
    pyyaml \
    ClusterShell \
    influxdb \
    libtmux \
    ibm_db \
    pex \
    flask
