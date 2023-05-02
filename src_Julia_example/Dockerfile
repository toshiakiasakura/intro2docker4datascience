FROM jupyter/datascience-notebook:lab-3.6.3

WORKDIR /workdir
EXPOSE 8888

ENV JULIA_PROJECT=/workdir
RUN julia -e 'using Pkg; Pkg.activate(".")'
COPY ./Manifest.toml Manifest.toml
COPY ./Project.toml Project.toml
RUN julia -e 'using Pkg; Pkg.instantiate()'

ENV JULIA_NUM_THREADS=4

COPY ./freqtables.so freqtables.so
RUN julia -e 'using IJulia; \
    sysimage = joinpath(@__DIR__, "freqtables.so"); \
    installkernel("Julia-freqtables", "--project-@.", "--sysimage=$(sysimage)")'
