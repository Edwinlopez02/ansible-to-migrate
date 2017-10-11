FROM ubuntu:16.04

RUN apt-get update && apt-get full-upgrade -y

RUN apt-get install -y openssh-server python python-pip

RUN mkdir /var/run/sshd

COPY authorized_keys /root/.ssh/authorized_keys

RUN ["chmod","0600","/root/.ssh/authorized_keys"]

CMD ["/usr/sbin/sshd", "-D"]  
