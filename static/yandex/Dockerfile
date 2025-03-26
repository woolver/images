ARG VERSION

FROM golang:1.22-bullseye as go

COPY devtools /devtools

RUN \
    apt-get update && \
    apt-get install -y upx-ucl && \
    cd /devtools && \
    go test -race && \
    GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" && \
    upx /devtools/devtools

FROM selenoid/dev_yandex:$VERSION

ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
COPY --from=go /devtools/devtools /usr/bin/
COPY policies.json /etc/opt/yandex/policies/managed/
COPY yandexdriver /usr/bin/
COPY entrypoint.sh /

RUN \
    chmod +x /usr/bin/yandexdriver && \
    chown -R selenium:nogroup /etc/opt/yandex/policies/managed/ && \
    echo "cookie-file = ~/.config/pulse/cookie" >> /etc/pulse/client.conf

USER selenium

EXPOSE 4444
ENTRYPOINT ["/entrypoint.sh"]
