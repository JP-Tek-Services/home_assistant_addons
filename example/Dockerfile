ARG BUILD_FROM
FROM $BUILD_FROM

SHELL ["/bin/bash", "-o", "pipefail", "-c"]


ARG BUILD_ARCH

ARG DEBIAN_FRONTEND=noninteractive

#
CMD [ "/run.sh" ]

# Build arguments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="example" \
    io.hass.description="Addon to run example with Home Assistant" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Joshua Peterson <https://github.com/Jpeterson37>" \
    org.opencontainers.image.title="example" \
    org.opencontainers.image.description="Addon to run example with Home Assistant" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Joshua Peterson <https://github.com/Jpeterson37>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/JP-Tek-Services/home_assistant_addons" \
    org.opencontainers.image.source="https://github.com/JP-Tek-Services/addon-example" \
    org.opencontainers.image.documentation="https://github.com/JP-Tek-Services/addon-example/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}

