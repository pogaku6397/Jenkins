FROM centos:7
RUN yum install openssh-server -y && \
    useradd remote_user && \
    echo "password" | passwd remote_user --stdin && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh
COPY remote-key.pub /home/remote_user/.ssh/authorized_keys
COPY aws-s3.sh /tmp/aws-s3.sh
RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys && \
    yum -y install mysql && \
    yum -y install epel-release && \
    yum -y install python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install awscli
RUN /usr/bin/ssh-keygen -A
EXPOSE 22
RUN rm -rf /run/nologin
CMD /usr/sbin/sshd -D
