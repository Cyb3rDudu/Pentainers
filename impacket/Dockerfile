FROM python:alpine

RUN apk --update --no-cache add \
    zlib-dev \
    musl-dev \
    libc-dev \
    gcc \
    libffi-dev \
    openssl-dev \
    && rm -rf /var/cache/apk/* \
    && mkdir -p /opt/impacket

COPY impacket /opt/impacket
WORKDIR /opt/impacket

RUN pip install .
WORKDIR /opt/impacket/examples

ENTRYPOINT ["python"]