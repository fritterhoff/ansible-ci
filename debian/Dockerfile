FROM debian:buster

# Labels.
LABEL maintainer="ritterho@hm.edu" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.name="fritterhoff/ansible-ci" \
    org.label-schema.description="Docker Image containing Ansible" \
    org.label-schema.url="https://github.com/fritterhoff/ansible-ci" \
    org.label-schema.vcs-url="https://github.com/fritterhoff/ansible-ci" \
    org.label-schema.docker.cmd="docker run --rm -it ~/.ssh/:/root/.ssh/ fritterhoff/ansible-ci:debian"


RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y python3-pip sshpass git openssh-client curl unzip && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean
    
RUN pip3 install --upgrade pip cffi && \
    pip install ansible==4.3.0 && \
    ansible-galaxy collection install community.docker community.general && \
    rm -rf /root/.cache/pip

RUN curl -L https://releases.hashicorp.com/terraform/1.0.3/terraform_1.0.3_linux_amd64.zip -o /tmp/terraform.zip && \ 
    unzip /tmp/terraform.zip -d /tmp && \
    mv /tmp/terraform /usr/local/bin/ && \
    rm -rf /tmp/terraform.zip