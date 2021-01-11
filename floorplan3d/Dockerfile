ARG BUILD_FROM=hassioaddons/base:8.0.6
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003
RUN \
    apk add --no-cache --virtual .build-dependencies \
        unzip=6.0-r8 \
        wget=1.20.3-r1 \
    \
    && apk add --no-cache \
        lua-resty-http=0.15-r0 \
        nginx-mod-http-lua=1.18.0-r1 \
        nginx=1.18.0-r1 \
    \
    && wget "https://github.com/vicfergar/Floorplan3D/releases/download/v0.1-alpha/wwwroot.zip" \
    && mkdir -p /var/www/html \
    && unzip -d /var/www/html "wwwroot.zip" \
    && rm "wwwroot.zip" \
    \
    && apk del --no-cache --purge .build-dependencies \
    && rm -fr \
        /etc/nginx

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Floorplan 3D" \
    io.hass.description="3D Floorplan viewer add-on that hosts a WebGL2 wiewer made with Wave Engine 3.1 Preview 2" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Victor Ferrer <vicfergar@gmail.com>" \
    org.opencontainers.image.title="Floorplan 3D" \
    org.opencontainers.image.description="3D Floorplan viewer add-on that hosts a WebGL2 wiewer made with Wave Engine 3.1 Preview 2" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Victor Ferrer <vicfergar@gmail.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/vicfergar/addon-floorplan3d" \
    org.opencontainers.image.documentation="https://github.com/vicfergar/addon-floorplan3d/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
