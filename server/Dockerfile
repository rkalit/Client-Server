FROM ubuntu:18.04

LABEL maintainer="ruli"

RUN apt-get -y update && apt-get install -y openssh-server
RUN apt-get clean
RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN apt-get install -y rsyslog && apt-get install -y rsync

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]