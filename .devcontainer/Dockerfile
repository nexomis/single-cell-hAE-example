FROM mcr.microsoft.com/devcontainers/base:bookworm

# https://docs.posit.co/resources/install-r/
# https://irkernel.github.io/installation/#linux-panel 
# libzmq3-dev libcurl4-openssl-dev libssl-dev jupyter-core jupyter-client 

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get -y install --no-install-recommends \
    gdebi-core \
    libzmq3-dev libcurl4-openssl-dev libssl-dev jupyter-core jupyter-client \
  && export R_VERSION=4.3.3 \
  && curl -O https://cdn.rstudio.com/r/debian-12/pkgs/r-${R_VERSION}_1_amd64.deb \
  && gdebi --n r-${R_VERSION}_1_amd64.deb \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R \
  && ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript \
  && Rscript -e "install.packages(c('repr', 'IRdisplay', 'IRkernel'), repos = 'http://cran.rstudio.com/')" \
  && Rscript -e "IRkernel::installspec(user = FALSE)"

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get install -y libglpk-dev libpng-dev libfontconfig1-dev libharfbuzz-dev libfribidi-dev libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev \
  && Rscript -e "install.packages(c('Seurat', 'hdf5r', 'devtools', 'BiocManager'), repos='http://cran.us.r-project.org', ask = F)" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && Rscript -e "devtools::install_github('satijalab/seurat-data')" \
  && Rscript -e "devtools::install_github('immunogenomics/presto')" \
  && Rscript -e "BiocManager::install('SingleR')" \
  && Rscript -e "BiocManager::install('celldex')" \
  && Rscript -e "BiocManager::install('SingleCellExperiment')"

RUN Rscript -e "install.packages(c('ggExtra'))" \
  && Rscript -e "devtools::install_github('guokai8/rcellmarker')" \
  && Rscript -e "devtools::install_github('rx-li/EasyCellType')" \
  && Rscript -e "install.packages(c('SoupX'), repos = 'http://cran.rstudio.com/')" \
