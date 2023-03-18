FROM ubuntu:latest

RUN \
apt-get update -y && \
apt-get install unzip -y && \
apt-get install wget -y && \
apt-get install vim -y && \
apt-get install curl -y && \
apt-get install git -y && \
apt-get install mandoc -y 

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
RUN wget https://releases.hashicorp.com/terraform/1.3.0/terraform_1.3.0_linux_amd64.zip
RUN unzip terraform_1.3.0_linux_amd64.zip
RUN mv terraform /usr/local/bin/
RUN terraform --version 

################################
# Install Terragrunt
################################
RUN wget --progress=dot:mega https://github.com/gruntwork-io/terragrunt/releases/download/v0.40.0/terragrunt_linux_amd64
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

################################
# Setup ZSH
################################
# https://github.com/deluan/zsh-in-docker
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.5/zsh-in-docker.sh)" -- \
-p "https://github.com/zsh-users/zsh-autosuggestions" -p "history-substring-search" \
-a 'bindkey "\$terminfo[kcuu1]" history-substring-search-up' \
-a 'bindkey "\$terminfo[kcud1]" history-substring-search-down'

RUN echo 'alias tg="/usr/local/bin/terragrunt"' >> ~/.zshrc
RUN echo 'alias tf="/usr/local/bin/terraform"' >> ~/.zshrc

# Switch default shell to ZSH
RUN chsh -s ~/.zshrc

CMD [ "zsh" ]