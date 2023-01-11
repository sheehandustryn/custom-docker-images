FROM ubuntu:latest
SHELL ["/bin/bash", "-c"]
RUN apt update && apt install -y ca-certificates curl unzip && \
  curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.22.6/2022-03-09/bin/linux/amd64/kubectl && \
  curl -o aws-iam-authenticator https://s3.us-west-2.amazonaws.com/amazon-eks/1.21.2/2021-07-05/bin/linux/amd64/aws-iam-authenticator && \
  curl -o awscliv2.zip https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip  && \
  chmod +x ./kubectl && \
  mv ./kubectl /usr/local/bin && \
  unzip awscliv2.zip && \
  ./aws/install && \
  chmod +x ./aws-iam-authenticator && \
  mv ./aws-iam-authenticator /usr/local/bin && \
  adduser --shell /bin/bash --uid 1002 --disabled-login --home /home/user user && \
  mkdir -p /home/user/.kube
COPY ./config-config.yml /home/user/.kube/cluster-config
RUN chown -R user:user /home/user/.kube
USER user
WORKDIR /home/user
