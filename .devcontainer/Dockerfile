FROM mambaorg/micromamba:1-bullseye
ARG USER=snek
ARG UID=1000
ARG GID=1000

USER root
RUN addgroup --gid ${GID} ${USER} && adduser --disabled-password --gecos '' --uid ${UID} --gid ${GID} ${USER}
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       curl \
    && apt-get clean \
    && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log

USER ${USER}
WORKDIR /workspace
RUN <<-EOF
    curl -L https://api.github.com/repos/snakemake/snakemake-tutorial-data/tarball -o snakemake-tutorial-data.tar.gz
    tar --wildcards -xf snakemake-tutorial-data.tar.gz --strip 1 "*/data" "*/environment.yaml"
    rm snakemake-tutorial-data.tar.gz
    micromamba install -y -n base -f environment.yaml
EOF

LABEL org.opencontainers.image.source https://github.com/radusuciu/snakemake-tutorial
