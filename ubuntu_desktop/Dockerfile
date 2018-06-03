FROM ubuntu

#arg only sets env variable atbuild time

# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start.
RUN sed -i "s/^exit 101$/exit 0/" /usr/sbin/policy-rc.d

RUN apt-get update	

RUN  apt-get install -y \
	#ubuntu-minimal \
	#ubuntu-standard \
	sudo \
	apt-utils \
	#libpam-systemd \
	policykit-1

RUN DEBIAN_FRONTEND="noninteractive"  apt-get install -y ubuntu-desktop --no-install-recommends

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/cuser && \
    echo "cuser:x:${uid}:${gid}:cuser,,,:/home/cuser:/bin/bash" >> /etc/passwd && \
    echo "cuser:x:${uid}:" >> /etc/group && \
    echo "cuser ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/cuser && \
    chmod 0440 /etc/sudoers.d/cuser && \
    chown ${uid}:${gid} -R /home/cuser

USER cuser
ENV HOME /home/cuser
#ENV DEBIAN_FRONTEND teletype
