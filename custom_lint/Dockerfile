FROM alpine:3.15 as builder

RUN apk add --no-cache \
	bc \
	gcc \
	libffi-dev \
	make \
	musl-dev \
	openssl-dev \
	py3-pip \
	python3 \
	python3-dev

RUN pip3 install --ignore-installed coverage \
	mock \
	nose \
	unittest2 \
	pylint \
	pycodestyle \
	argparse \
	requests \
	influxdb \
	libtmux \
	pyyaml \
	Sphinx \
	sphinx_rtd_theme \
	sphinx-prompt \
	sphinxcontrib-httpdomain \
	Sphinx-Substitution-Extensions \
	ibm_db \
	boto3

# Separating CLusterShell install for mysterious reasons..
RUN pip3 install --ignore-installed ClusterShell

RUN find /usr/lib/ -name '__pycache__' -print0 | xargs -0 -n1 rm -rf \
	&& find /usr/lib/ -name '*.pyc' -print0 | xargs -0 -n1 rm -rf

FROM alpine:3.15 as production

RUN set -x \
	&& apk add --no-cache python3 py3-pip \
	&& ln -sf /usr/bin/python3 /usr/bin/python \
	&& ln -sf /usr/bin/pip3 /usr/bin/pip \
	&& find /usr/lib/ -name '__pycache__' -print0 | xargs -0 -n1 rm -rf \
	&& find /usr/lib/ -name '*.pyc' -print0 | xargs -0 -n1 rm -rf

COPY --from=builder /usr/lib/python3.9/site-packages/ /usr/lib/python3.9/site-packages/
COPY --from=builder /usr/bin/pylint /usr/bin/pylint
COPY --from=builder /usr/bin/pycodestyle /usr/bin/pycodestyle
WORKDIR /data
