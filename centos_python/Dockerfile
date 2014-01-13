FROM centos

RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN yum install -y passwd
RUN yum install -y sudo
RUN yum install -y gcc
RUN yum install -y gcc-c++
RUN yum install -y make
RUN yum install -y vim
RUN yum install -y git
RUN yum install --enablerepo=epel -y mosh
RUN yum install -y openssl-devel
RUN yum install -y zlib-devel
RUN yum install -y readline-devel
RUN yum install -y sqlite-devel
RUN yum install -y bzip2-devel
RUN yum install -y libevent-devel
RUN yum install -y openssh
RUN yum install -y openssh-server
RUN yum install -y openssh-clients

RUN useradd ore
RUN passwd -f -u ore
RUN mkdir -p /home/ore/.ssh
ADD ./authorized_keys /home/ore/.ssh/
RUN chown -R ore. /home/ore/.ssh
RUN chmod 700 /home/ore/.ssh
RUN chmod 600 /home/ore/.ssh/authorized_keys
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN echo "ore    ALL=(ALL)       ALL" >> /etc/sudoers.d/ore

RUN git clone git://github.com/yyuu/pyenv.git /home/ore/.pyenv
RUN echo 'export PYENV_ROOT="${HOME}/.pyenv"' >> /home/ore/.bashrc
RUN echo 'if [ -d "${PYENV_ROOT}" ]; then' >> /home/ore/.bashrc
RUN echo '    export PATH=${PYENV_ROOT}/bin:$PATH' >> /home/ore/.bashrc
RUN echo '    eval "$(pyenv init -)"' >> /home/ore/.bashrc
RUN echo 'fi' >> /home/ore/.bashrc
RUN cd /home/ore/.pyenv/plugins; git clone git://github.com/yyuu/pyenv-virtualenv.git
RUN chown -R ore. /home/ore/.pyenv
RUN su ore -c "/home/ore/.pyenv/bin/pyenv install 3.3.3"

RUN /etc/init.d/sshd start
RUN /etc/init.d/sshd stop

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

