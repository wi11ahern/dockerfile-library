FROM ubuntu:latest

RUN \
apt-get update -y && \
apt-get install unzip -y && \
apt-get install wget -y && \
apt-get install vim -y && \
apt-get install -y git

################################
# Setup SSH
################################
ARG SSH_PRIVATE_KEY
ARG SSH_PUBLIC_KEY
RUN mkdir -p /root/.ssh/
RUN echo "${SSH_PRIVATE_KEY}" > /root/.ssh/id_rsa
RUN echo "${SSH_PUBLIC_KEY}" > /root/.ssh/id_rsa.pub
RUN chmod 600 /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa.pub
RUN ssh-keyscan github.com > /root/.ssh/known_hosts

################################
# Install Terraform
################################
RUN wget https://releases.hashicorp.com/terraform/0.14.5/terraform_0.14.5_linux_amd64.zip
RUN unzip terraform_0.14.5_linux_amd64.zip
RUN mv terraform /usr/local/bin/
RUN terraform --version 

################################
# Install Terragrunt
################################
RUN wget --progress=dot:mega https://github.com/gruntwork-io/terragrunt/releases/download/v0.27.3/terragrunt_linux_amd64
RUN ls -lart
RUN mv terragrunt_linux_amd64 /usr/local/bin/terragrunt
RUN chmod +x /usr/local/bin/terragrunt
RUN terragrunt --version

################################
# Install Python
################################
RUN apt-get install -y python3-pip
RUN pip3 install --upgrade pip
RUN python3 -V
RUN pip --version

################################
# Install AWS CLI
################################
RUN pip install awscli --upgrade --user
ENV PATH=~/.local/bin:$PATH
RUN mkdir ~/.aws && touch ~/.aws/credentials

