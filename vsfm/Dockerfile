FROM quay.io/fish/sfm-base

ENV  VSFM_URL  http://ccwu.me/vsfm/download/VisualSFM_linux_64bit.zip
ENV  VSFM_SHA1 9fe79d91ec5f623a45ca98a3de68f500636ab5bb

ENV  BUILD_DEPS curl unzip make g++ libgtk2.0-dev libgl1-mesa-dev libglu1-mesa-dev

RUN apt-get -qy install libgtk2.0 $BUILD_DEPS \
    && curl -L -o /tmp/vsfm.zip $VSFM_URL \
    && echo "$VSFM_SHA1  /tmp/vsfm.zip" | sha1sum -c \
    && unzip /tmp/vsfm.zip && rm /tmp/vsfm.zip \
    && cd vsfm \
    && rm -rf bin/* && make \
    && mv bin/VisualSFM /usr/local/bin \
    && apt-get -qy purge --auto-remove $BUILD_DEPS \
    && ln -s /data/log /usr/local/bin/log # vsfm logs to bin dir, not cwd..

VOLUME /data
WORKDIR /data
ENTRYPOINT [ "/usr/local/bin/VisualSFM" ]
