FROM ghcr.io/dodas-ts/dodas-iam-client-rec:v0.0.6-pre3 as REGISTRATION

FROM jupyterhub/k8s-hub:2.0.1-0.dev.git.6105.hb969fa50

USER root

RUN pip3 install pyjwt

RUN apt-get update && apt-get -y install vim sudo git curl ca-certificates

RUN curl -k  https://raw.githubusercontent.com/DODAS-TS/dodas-apps/master/logo.png -o /etc/logo.png

RUN echo "jovyan ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
       rm /bin/sh && \
       ln -s /bin/bash /bin/sh

RUN mkdir -p .init

COPY --from=REGISTRATION /usr/local/bin/dodas-IAMClientRec /srv/.init/dodas-IAMClientRec

CMD ["/usr/bin/start.sh", "jupyterhub"]
