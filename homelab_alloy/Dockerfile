ARG BUILD_FROM
FROM ${BUILD_FROM}

RUN apt-get update && apt-get install -y --no-install-recommends curl jq unzip ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Alloy fest auf eine Version, Download per SHA256 geprüft (Werte aus SHA256SUMS des Releases)
ARG ALLOY_VERSION=1.21.3
ARG ALLOY_SHA256=50d23af2d0f98c00beac6ce9a365693e60f87fb76b6cad6fe1d161e80588af6d
RUN set -eux; \
    curl -fsSL "https://github.com/grafana/alloy/releases/download/v${ALLOY_VERSION}/alloy-linux-amd64.zip" -o /tmp/alloy.zip; \
    echo "${ALLOY_SHA256}  /tmp/alloy.zip" | sha256sum -c -; \
    unzip /tmp/alloy.zip -d /tmp/alloy; \
    install -m 0755 /tmp/alloy/alloy-linux-amd64 /usr/bin/alloy; \
    rm -rf /tmp/alloy.zip /tmp/alloy

# Root der step-ca (öffentlich), damit Alloy loki.arnold.home vertraut
COPY homelab-root-ca.crt /usr/local/share/ca-certificates/homelab-root-ca.crt
RUN update-ca-certificates

COPY rootfs /
