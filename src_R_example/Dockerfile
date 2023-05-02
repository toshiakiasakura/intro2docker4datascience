FROM jupyter/datascience-notebook:lab-3.6.3

WORKDIR /workdir
EXPOSE 8888

RUN mamba install -c conda-forge \
      r-finalfit \
      r-gtsummary \
      -y

