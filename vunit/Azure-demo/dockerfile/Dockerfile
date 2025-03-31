# ------------------------------------------------------------------------------
# Build Stage
# ------------------------------------------------------------------------------

FROM ubuntu:23.04 as build-image

LABEL autodelete="true"

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        wget \
        ca-certificates \
        python3 \
        python3-pip \
        python3-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --break-system-packages \
        lxml \
        vunit_hdl \
        pycryptodome

# ------------------------------------------------------------------------------
# Final Stage
# ------------------------------------------------------------------------------

FROM aldec/riviera-pro:latest

ENV PATH=/root/.local/bin:$PATH
ENV ALDEC_LICENSE_FILE=9393@127.0.0.1

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        python3 \
    && rm -rf /var/lib/apt/lists/*

COPY --from=build-image  /usr/local/lib /usr/local/lib
