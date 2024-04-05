# selecting the base ubuntu image for docker agent
FROM ubuntu:22.04


# update the package manager and install the dependencies
RUN yes | sudo apt-get update
RUN yes | sudo apt install git
RUN yes | sudo apt install python3
RUN yes | sudo apt install default-jdk
RUN yes | sudo apt install default-jre
RUN yes | sudo apt install openssh-server

# add a jenkins user with password
RUN sudo adduser --quiet jenkins
RUN sudo echo "jenkins:jenkins123" | chpasswd
RUN mkdir /home/jenkins/.m2

# copy the public key of jenkins server
RUN echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIL+hOoZbvvZSI8FfF+JXrAgMmz2O7myFBnjIAxnJGQXu Jenkins" > ~/.ssh/authorized_keys

# add the permissions to the filesystem
RUN chown -R jenkins:jenkins /home/jenkins/.m2 && chown -R jenkins:jenkins /home/jenkins/.ssh

# exposing port 22 for ssh to container from jenkins server
EXPOSE 22

# run the openssh server
CMD [ "/usr/bin/sshd","-D" ]