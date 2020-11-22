FROM chocobozzz/peertube:production-buster

# Add plugins
RUN set -ex; \
    yarn install; \
    node dist/scripts/plugin/install.js -n peertube-plugin-auth-ldap; \
    node dist/scripts/plugin/install.js -n peertube-plugin-matomo; \
    node dist/scripts/plugin/install.js -n peertube-theme-dark; \
    node dist/scripts/plugin/install.js -n peertube-plugin-social-sharing; \
    node dist/scripts/plugin/install.js -n peertube-plugin-upload-limits; \
    node dist/scripts/plugin/install.js -n peertube-plugin-webapp-manifest

COPY ./custom-environment-variables.yaml /app/support/docker/production/config/custom-environment-variables.yaml

# Arguments to label built container
ARG VCS_REF
ARG BUILD_DATE
ARG VERSION=production

# Keep track of image version
RUN set -ex; \
    mkdir -p '/app/docker'; \
    echo "${VERSION} ${VCS_REF} ${BUILD_DATE}" > '/app/docker/.docker-version'

# Container labels (http://label-schema.org/)
# Container annotations (https://github.com/opencontainers/image-spec)
LABEL maintainer="Monogramm maintainers <opensource at monogramm dot io>" \
      product="PeerTube" \
      version=$VERSION \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/Monogramm/docker-peertube" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="PeerTube" \
      org.label-schema.description="ActivityPub-federated video streaming platform using P2P directly in your web browser" \
      org.label-schema.url="https://joinpeertube.org/" \
      org.label-schema.vendor="Framasoft" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0" \
      org.opencontainers.image.revision=$VCS_REF \
      org.opencontainers.image.source="https://github.com/Monogramm/docker-peertube" \
      org.opencontainers.image.created=$BUILD_DATE \
      org.opencontainers.image.title="PeerTube" \
      org.opencontainers.image.description="ActivityPub-federated video streaming platform using P2P directly in your web browser" \
      org.opencontainers.image.url="https://joinpeertube.org/" \
      org.opencontainers.image.vendor="Framasoft" \
      org.opencontainers.image.version=$VERSION \
      org.opencontainers.image.authors="Monogramm maintainers <opensource at monogramm dot io>"
