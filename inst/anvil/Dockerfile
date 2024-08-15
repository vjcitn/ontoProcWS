FROM us.gcr.io/broad-dsp-gcr-public/anvil-rstudio-bioconductor:3.19.0

WORKDIR /home/rstudio

COPY --chown=rstudio:rstudio . /home/rstudio/

RUN Rscript -e "BiocManager::install(ask=FALSE); BiocManager::install(c('reticulate', 'devtools', 'remotes', 'BiocStyle', 'magick'), ask=FALSE); BiocManager::install('ccb-hms/gwasCatSearch')"

ENV RETICULATE_PYTHON=/usr/bin/python3
RUN Rscript -e "BiocManager::install(c('vjcitn/ontoProc')); reticulate::py_config()" && /usr/bin/pip3 install owlready2

## now build for the workshop
RUN Rscript -e "devtools::install('.', dependencies=FALSE, build_vignettes=FALSE, repos = BiocManager::repositories()); library(ontoProc); example('plot.owlents')" # ensure cache started

