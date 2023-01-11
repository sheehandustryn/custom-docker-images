FROM openjdk:11 as sbt-download
RUN curl -L -o /tmp/sbt-archive.tgz https://github.com/sbt/sbt/releases/download/v1.5.5/sbt-1.5.5.tgz && \
    tar -xf /tmp/sbt-archive.tgz --directory /tmp && \
    rm /tmp/sbt-archive.tgz

FROM openjdk:11 as docker-compose-download
COPY --from=sbt-download /tmp /tmp
RUN mkdir /docker
RUN curl -L -o /docker/docker-compose "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)"


FROM openjdk:11 as runner
RUN useradd -u 1002 --create-home user
COPY --from=docker-compose-download /tmp /home/user
COPY --from=docker-compose-download /docker /docker
COPY --from=docker-compose-download /docker/docker-compose /home/user/bin/docker-compose
RUN apt-get dist-upgrade && \
    apt update -y && \
    apt install postgresql-client -y && \
    chown -R user:user /home/user/bin
USER user
ENV PATH $PATH:/home/user/sbt/bin:/home/user/bin
