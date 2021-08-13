FROM docker.io/fluxcd/flux:1.21.1

RUN echo "== Installing dependencies" \
  && apk update \
  && apk add python3 py3-pip \
  && pip3 install pyyaml \
  && mkdir /root/.config \
  && echo "done"

ADD plugins /root/.config
