FROM alpine:3.15
LABEL maintainer="Robert Carlson <tech@sheehandustryn.com"
LABEL updated=_at="2022-04-12"
COPY kafkacat-1.6.0-r0.apk .
COPY sgerrand.rsa.pub /etc/apk/keys/sgerrand.rsa.pub
RUN apk update && \
    apk add --no-cache openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/v3.15/community && \
    apk add --no-cache bash curl git bind-tools iputils busybox-extras postgresql-client alpine-sdk python3-dev py-pip py-cffi krb5 ca-certificates wget nmap kafkacat-1.6.0-r0.apk
WORKDIR /usr/bin
RUN curl https://archive.apache.org/dist/kafka/2.7.1/kafka_2.12-2.7.1.tgz -o kafka_2.12-2.7.1.tgz && tar -xvzf kafka_2.12-2.7.1.tgz
SHELL ["/bin/bash", "-l", "-c"]
RUN adduser -s /bin/bash -h /asdf -D asdf
ENV PATH="${PATH}:/asdf/.asdf/shims:/asdf/.asdf/bin:/asdf/.local/bin"
USER asdf
WORKDIR /asdf
RUN git clone --depth 1 https://github.com/asdf-vm/asdf.git $HOME/.asdf && \
    echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc && \
    echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.profile && \
    source ~/.bashrc && \
    mkdir -p $HOME/.asdf/toolset && \
    asdf plugin-add awscli $(< $HOME/.asdf/toolset/awscli/plugin-repo) && \
    asdf plugin-add helm $(< $HOME/.asdf/toolset/helm/plugin-repo) && \
    asdf plugin-add helmfile $(< $HOME/.asdf/toolset/helmfile/plugin-repo) && \
    asdf plugin-add terraform $(< $HOME/.asdf/toolset/terraform/plugin-repo) && \
    asdf plugin-add terragrunt $(< $HOME/.asdf/toolset/terragrunt/plugin-repo) && \
    asdf plugin add redis-cli $(< $HOME/.asdf/toolset/redis-cli/plugin-repo) && \
    asdf install awscli latest && \
    asdf install helm latest && \
    asdf install helmfile latest && \
    asdf install terraform latest && \
    asdf install terragrunt latest && \
    asdf install redis-cli latest
