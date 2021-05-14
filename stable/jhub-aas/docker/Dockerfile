FROM ghcr.io/dodas-ts/dodas-iam-client-rec:v0.0.5 as REGISTRATION

FROM jupyterhub/k8s-hub:0.11.1

USER root

RUN apt-get update

# Install required apt packages for all the extensions
RUN apt-get -y install vim sudo git curl ca-certificates

RUN curl -k "https://crt.sh/?d=2475254782" -o /usr/local/share/ca-certificates/ca.crt && \                                      
    update-ca-certificates 

RUN curl -k https://baltig.infn.it/infn-cloud/web-site/-/raw/master/imgs/INFN_Cloud/Sito/selezione_sito_cloud/INFN_Cloud_logo_home.png -o /etc/logo.png

RUN echo "jovyan ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Use bash instead of dash
RUN rm /bin/sh && \
    ln -s /bin/bash /bin/sh

USER $NB_UID

RUN mkdir -p .init

COPY --from=REGISTRATION /usr/local/bin/dodas-IAMClientRec /srv/.init/dodas-IAMClientRec


CMD ["/usr/bin/start.sh", "jupyterhub"]
