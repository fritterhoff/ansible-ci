# pull base image
FROM alpine:3

# Labels.
LABEL maintainer="ritterho@hm.edu" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.name="fritterhoff/ansible-ci" \
    org.label-schema.description="Docker Image containing Ansible" \
    org.label-schema.url="https://github.com/fritterhoff/ansible-ci" \
    org.label-schema.vcs-url="https://github.com/fritterhoff/ansible-ci" \
    org.label-schema.docker.cmd="docker run --rm -it ~/.ssh/:/root/.ssh/ fritterhoff/ansible-ci:alpine"

RUN apk --no-cache add sudo python3 py3-pip openssl ca-certificates sshpass openssh-client rsync git && \
    apk --no-cache add --virtual build-dependencies python3-dev libffi-dev musl-dev gcc cargo openssl-dev build-base && \
    pip3 install --upgrade pip wheel && \
    pip3 install --upgrade cryptography cffi && \
    pip3 install ansible==4.4.0 && \
    ansible-galaxy collection install community.docker community.general && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/* && \
    rm -rf /root/.cache/pip && \
    rm -rf /root/.cargo