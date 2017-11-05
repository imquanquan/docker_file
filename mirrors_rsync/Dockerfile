# BUILD Stage
FROM alpine:latest AS builder

LABEL maintainer="imquanquan <imquanquan99@gmail.com>"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk update && apk add --no-cache git && rm -rf /var/cache/apk/*
RUN git clone https://github.com/SCAULUG/Mirrors-Scripts.git


# DIST Stage
FROM alpine:latest

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk update && apk add --no-cache dcron bash rsync python3 && rm -rf /var/cache/apk/*

RUN pip3 install -r https://bitbucket.org/pypa/bandersnatch/raw/stable/requirements.txt
RUN touch /var/log/pypi.log
RUN mkdir /mirrors


COPY --from=builder /Mirrors-Scripts /Mirrors-Scripts
COPY ./default.conf /etc/bandersnatch.conf
COPY ./rsync-cron /etc/crontabs/root

CMD crond && tail -f /var/log/pypi.log
