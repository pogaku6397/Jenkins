FROM centos:7
RUN yum install openssh-server -y && \
    useradd remote_user && \
    echo "password" | passwd remote_user --stdin && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh
COPY remote-key.pub /home/remote_user/.ssh/authorized_keys
RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys
RUN /usr/bin/ssh-keygen -A
EXPOSE 22
RUN rm -rf /run/nologin
CMD /usr/sbin/sshd -D
