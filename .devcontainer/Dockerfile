FROM mcr.microsoft.com/devcontainers/base:bookworm

# https://docs.posit.co/resources/install-r/
# https://irkernel.github.io/installation/#linux-panel 
# libzmq3-dev libcurl4-openssl-dev libssl-dev jupyter-core jupyter-client 

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get -y install --no-install-recommends \
    gdebi-core \
    libzmq3-dev libcurl4-openssl-dev libssl-dev jupyter-core jupyter-client \
  && export R_VERSION=4.2.3 \
  && curl -O https://cdn.rstudio.com/r/debian-12/pkgs/r-${R_VERSION}_1_amd64.deb \
  && gdebi --n r-${R_VERSION}_1_amd64.deb \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R \
  && ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript \
  && Rscript -e "install.packages(c('repr', 'IRdisplay', 'IRkernel'), repos = 'http://cran.rstudio.com/')" \
  && Rscript -e "IRkernel::installspec(user = FALSE)"

