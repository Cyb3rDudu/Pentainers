FROM python:alpine

COPY run.sh /webdav/
WORKDIR /webdav/

RUN pip install wsgidav cheroot \
    && mkdir -p /webdav/share && mkdir -p /srv/data/share \
    && chmod +x /webdav/run.sh

ENTRYPOINT [ "/webdav/run.sh" ]