FROM python:3.9-alpine

RUN apk add --no-cache py3-pip openssl

COPY requirements.txt .

RUN apk add --no-cache --virtual build-deps \
    python3-dev openssl-dev libffi-dev musl-dev gcc rust cargo git && \
    pip install -r requirements.txt --break-system-packages && \
    apk del build-deps

RUN mkdir -p /etc/pykmip \
    mkdir -p /etc/pykmip/policy \
    mkdir -p /var/lib/certs \
    mkdir -p /var/lib/state \
    mkdir -p /var/log/pykmip

COPY server.conf /etc/pykmip

COPY policy.json /etc/pykmip/policy

#RUN ln -sf /dev/stdout /var/log/pykmip/server.log

EXPOSE 5696

ENTRYPOINT pykmip-server
