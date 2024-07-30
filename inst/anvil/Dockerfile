FROM us.gcr.io/broad-dsp-gcr-public/anvil-rstudio-bioconductor:3.19.0

WORKDIR /home/rstudio

COPY --chown=rstudio:rstudio . /home/rstudio/

# setup

USER rstudio
RUN Rscript -e "BiocManager::install(ask=FALSE)"
RUN Rscript -e "BiocManager::install(c('reticulate', 'devtools', 'remotes', 'BiocStyle', 'magick'), ask=FALSE)"
RUN Rscript -e "BiocManager::install('ccb-hms/gwasCatSearch')"
ENV RETICULATE_PYTHON=/usr/bin/python3
RUN Rscript -e "BiocManager::install(c('vjcitn/ontoProc'))"
RUN Rscript -e "reticulate::py_config()"
RUN /usr/bin/pip3 install owlready2
#
## now build for the workshop
RUN Rscript -e "devtools::install('.', dependencies=FALSE, build_vignettes=FALSE, repos = BiocManager::repositories())"
RUN Rscript -e "library(ontoProc); example('plot.owlents')" # ensure cache started
USER root
