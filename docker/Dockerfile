FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive

# Install SSH server
RUN apt-get update && apt-get install -y openssh-server python3

# Create SSH directory and set permissions
RUN mkdir -p /root/.ssh
RUN chmod 700 /root/.ssh

# Copy the authorized_keys file
COPY docker/ssh/authorized_keys /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/authorized_keys

# Setup SSH server
RUN mkdir /var/run/sshd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config

# Disable password authentication
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

WORKDIR /srv/app

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
