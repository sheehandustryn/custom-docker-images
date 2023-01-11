FROM python:3.9-alpine3.15
RUN apk add --no-cache git bash curl cmd:envsubst
SHELL ["/bin/bash", "-c"]
RUN adduser -s /bin/bash -u 1002 -D -h /home/user user
RUN pip install awscli
USER user
WORKDIR /home/user
RUN git clone  --depth 1 https://github.com/asdf-vm/asdf.git ~/.asdf
ENV PATH="${PATH}:/home/user/.asdf/shims:/home/user/.asdf/bin"
RUN echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc
RUN echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.profile
RUN echo -e '\n export PATH=$PATH:$HOME/.local/bin' >> ~/.profile
RUN echo -e '\n export PATH=$PATH:$HOME/.local/bin' >> ~/.bashrc
RUN source ~/.bashrc
RUN asdf plugin add helm
RUN asdf plugin add kubectl
RUN asdf install helm latest
RUN asdf install kubectl latest
RUN asdf local helm latest
RUN asdf local kubectl latest
RUN helm plugin install https://github.com/databus23/helm-diff
RUN mkdir /home/gitlab-runner/.kube
COPY ./cluster-config.yml /home/user/.kube/cluster-config
