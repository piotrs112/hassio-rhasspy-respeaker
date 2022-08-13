FROM rhasspy/rhasspy:2.5.11
LABEL maintainer="Michael Hansen <mike@rhasspy.org>"

ENV LANG C.UTF-8

RUN mkdir -p /var/cache/apt/armv7/archives/partial && \
	touch /var/cache/apt/armv7/archives/lock && \
	chmod 640 /var/cache/apt/armv7/archives/lock 
RUN apt-get -o Debug::pkgProblemResolver=true -o Debug::Acquire::http=true -f install -y --no-install-recommends \
      git \
      alsa-utils \
      dkms \
      i2c-tools \
      libasound2-plugins
RUN git clone "https://github.com/respeaker/seeed-voicecard" \
    && cd seeed-voicecard \
    && chmod a+x ./install.sh \
    && rm -rf .git \
    && apt-get purge -y --auto-remove git

ENV CONFIG_PATH /data/options.json

COPY run.sh /

ENTRYPOINT ["/run.sh"]
