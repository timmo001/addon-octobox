ARG BUILD_FROM=hassioaddons/base-amd64:1.4.2
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Sets working directory
WORKDIR /opt

# Setup base
RUN \
    apk add --no-cache --virtual .build-dependencies \
        autoconf=2.69-r0 \
        bzip2-dev=1.0.6-r6 \
        curl-dev=7.60.0-r1 \
        g++=6.4.0-r5 \
        gcc=6.4.0-r5 \
        libsass-dev=3.4.7-r0 \
        libxml2-dev=2.9.7-r0 \
        libxslt-dev=1.1.31-r0 \
        make=4.2.1-r0 \
        mariadb-dev=10.1.32-r0 \
        postgresql-dev=10.4-r0 \
        zlib-dev=1.2.11-r1 \
    \
    && apk add --no-cache \
        bzip2=1.0.6-r6 \
        git=2.15.2-r0 \
        libsass=3.4.7-r0 \
        libxml2=2.9.7-r0 \
        libxslt=1.1.31-r0 \
        nginx=1.12.2-r3 \
        nodejs=8.9.3-r1 \
        postgresql-contrib=10.4-r0 \
        postgresql=10.4-r0 \
        ruby-bigdecimal@edge=2.5.1-r2 \
        ruby-bundler@edge=1.16.2-r0 \
        ruby-dev@edge=2.5.1-r2 \
        ruby-etc@edge=2.5.1-r2 \
        ruby-json@edge=2.5.1-r2 \
        ruby-rdoc@edge=2.5.1-r2 \
        ruby@edge=2.5.1-r2 \
        zlib=1.2.11-r1 \
    \
    && git clone --branch 3dcfb03 --depth=1 \
        https://github.com/octobox/octobox.git /opt \
    \
    && bundle install \
        --without test \
        production \
        --jobs 2 \
    \
    && mkdir -p /var/run/postgresql \
    \
    && addgroup octobox \
    && adduser -D -H -S -G octobox octobox \
    \
    && apk del --purge \
        .build-dependencies \
        ruby-dev

# TODO Move up
ENV LANG en_US.utf8

# Copy root filesystem
COPY rootfs /

# Build arugments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Octobox" \
    io.hass.description="Take back control of your GitHub notifications" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.label-schema.description="Take back control of your GitHub notifications" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Octobox" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://community.home-assistant.io/?u=frenck" \
    org.label-schema.usage="https://github.com/hassio-addons/addon-octobox/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/hassio-addons/addon-octobox" \
    org.label-schema.vendor="Community Hass.io Add-ons"