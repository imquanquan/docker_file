FROM ubuntu:latest

LABEL maintainer="imquanquan <imquanquan99@gmail.com>"

RUN apt-get update && \
	apt-get -y install --no-install-recommends \
		virtualenv rsync cron\
	&& \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN virtualenv --python=python3.5 bandersnatch  && \
		bandersnatch/bin/pip install -r https://bitbucket.org/pypa/bandersnatch/raw/stable/requirements.txt 

COPY ./rsync-cron /etc/cron.d/rsync-cron
COPY ./default.conf /etc/bandersnatch.conf
COPY ./Mirrors-Scripts /Mirrors-Scripts

RUN chmod 0644 /etc/cron.d/rsync-cron
RUN touch /var/log/pypi.log
RUN mkdir /mirrors

CMD cron && tail -f /var/log/pypi.log
