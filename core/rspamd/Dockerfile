# syntax=docker/dockerfile-upstream:1.4.3

# rspamd image
FROM base:debian

ARG VERSION=local
LABEL version=$VERSION

RUN set -euxo pipefail \
  ; apt update \
  ; DEBIAN_FRONTEND=noninteractive apt -y install --no-install-recommends rspamd \
  ; rm -fr /var/cache/apt /var/lib/apt \
  ; mkdir /run/rspamd \
  ; mkdir /overrides

COPY conf/ /conf/
COPY start.py /

RUN echo $VERSION >/version

#EXPOSE 11332/tcp 11334/tcp 11335/tcp
HEALTHCHECK --start-period=350s CMD curl -skfLo /dev/null http://localhost:11334/

VOLUME ["/var/lib/rspamd"]

CMD /start.py
