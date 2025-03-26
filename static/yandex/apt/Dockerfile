FROM browsers/base:7.4.2

ARG VERSION=25.2.1.939-1
ARG PACKAGE=yandex-browser-stable
ARG INSTALL_DIR=browser 

LABEL browser=yandex-browser-stable:$VERSION

RUN  \
        curl -s https://repo.yandex.ru/yandex-browser/YANDEX-BROWSER-KEY.GPG | apt-key add - && \
        echo 'deb [arch=amd64] https://repo.yandex.ru/yandex-browser/deb stable main' > /etc/apt/sources.list.d/yandex-browser.list && \
        apt-get update && \
        apt-get -y --no-install-recommends install yandex-browser-stable=$VERSION && \
        yandex-browser --version && \
        rm /etc/apt/sources.list.d/yandex-browser.list && \
        rm -Rf /tmp/* && rm -Rf /var/lib/apt/lists/*