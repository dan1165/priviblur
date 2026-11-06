FROM alpine:3.24
WORKDIR /priviblur

COPY ./.git/ ./.git/
COPY ./requirements.txt ./requirements.txt
COPY ./src/ ./src/
COPY ./assets/ ./assets/
COPY ./locales/ ./locales/

RUN apk add --no-cache git python3 py3-setuptools tini && \
    addgroup -g 1000 -S priviblur && \
    adduser -u 1000 -S priviblur -G priviblur && \
    apk add --no-cache py3-pip && \
    python3 -m pip install --no-cache-dir --break-system-packages -r requirements.txt && \
    python3 -m pip cache purge && \
    apk del py3-pip && \
    pybabel compile -d locales -D priviblur && \
    # chown is needed otherwise git will error out with "fatal: detected dubious ownership in repository at '/priviblur'"
    chown -R priviblur:priviblur /priviblur && \
    git config --global --add safe.directory /priviblur

ENV PYTHONUNBUFFERED=1
EXPOSE 8000
USER priviblur
ENTRYPOINT [ "/sbin/tini", "--"]
CMD [ "python3", "-m", "src.server" ]
