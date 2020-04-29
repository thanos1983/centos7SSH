FROM centos:7
ENV container docker

COPY ["repos/kubernetes.repo","/etc/yum.repos.d/kubernetes.repo"]

RUN set -x \
	&& yum -y update \
	&& yum -y install epel-release \
	&& yum -y install ansible openssh-server openssh-clients \
	&& yum clean all

RUN set -x \
	&& mkdir /var/run/sshd

RUN set -x \
	&& echo "root:root" | chpasswd

RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN /usr/bin/ssh-keygen -A

CMD ["/usr/sbin/sshd", "-D"]
