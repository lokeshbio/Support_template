# DOCKER FILE FOR SUPPORT PROJECT
# 2026 Lokesh Mano
FROM rocker/verse:4.5.3
LABEL Description="Dockerfile for NBIS support project template"
LABEL Maintainer="lokeshwaran.manoharan@nbis.se"
LABEL org.opencontainers.image.source="https://github.com/lokeshbio/Support_template"

ARG QUARTO_VERSION="1.10.18"

RUN apt-get update -y \
  && apt-get clean \
  && apt-get install --no-install-recommends -y \
  libxml2-dev \
  libssl-dev \
  libcurl4-openssl-dev \
  libudunits2-dev \
  libgdal-dev \
  libavfilter-dev \
  libprotobuf-dev \
  libjq-dev \
  libarchive-dev \
  cargo \
  curl \
  && curl -o quarto-linux-amd64.deb -L https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.deb 

RUN rm -rf /var/lib/apt/lists/* \
  && install2.r --error --skipinstalled remotes fontawesome here htmlTable leaflet readxl writexl \
  && rm -rf /tmp/downloaded_packages \
  && mkdir /project /.cache \
  && chmod 777 /project /.cache

RUN install2.r --error --skipinstalled plotly DT ggpubr ggrepel cowplot crosstalk BiocManager littler languageserver httpgd

RUN /usr/local/lib/R/site-library/littler/examples/installBioc.r --error phyloseq DESeq2 edgeR ComplexHeatmap clusterProfiler

RUN apt-get install -y python3

RUN ln -s /usr/bin/python3 /usr/bin/python & \
    ln -s /usr/bin/pip3 /usr/bin/pip

USER rstudio

RUN /bin/bash -c "echo \"PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\$ '\" >> /home/rstudio/.bashrc "

WORKDIR /project

CMD ["/bin/bash"] 