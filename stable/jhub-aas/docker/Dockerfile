FROM ghcr.io/tommasodiotalevi/dodas-iam-client-rec:test as REGISTRATION

FROM jupyterhub/k8s-hub:4.2.0

USER root

RUN pip3 install pyjwt

RUN pip3 install kubernetes

RUN curl -k  https://raw.githubusercontent.com/DODAS-TS/dodas-apps/master/logo.png -o /etc/logo.png

RUN echo "jovyan ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
       rm /bin/sh && \
       ln -s /bin/bash /bin/sh

RUN mkdir -p .init

COPY --from=REGISTRATION /usr/local/bin/dodas-IAMClientRec /srv/.init/dodas-IAMClientRec

CMD ["/usr/bin/start.sh", "jupyterhub"]
