# Docker for R language.

## Package install.
Since Jupyter's datascience notebook uses Linux kernel, 
R installation is slow and sometimes installation fails.  
The most simple solution for it is to use `conda` to install the package. 
Jupyter's datascience notebook have already `mamba` (C written version of `conda`), 
so use mamba to install the package.  
You can find R packages from the anaconda package repository.   
- [Anaconda R package repository](https://anaconda.org/r/repo)

For example, if you want to install `finalfit` package, 
write `RUN mamba install -c conda-forge r-finalfit -y`. 
`-y` option is required to install package without confirmation.

Alternative way is use `install2.r` which requires the use of `rocker` images. 
See the following post for the detail.  
- [Install R packages using docker file](https://stackoverflow.com/questions/45289764/install-r-packages-using-docker-file)

## Installed packages
You can check pre-installed packages in jupyter's datascience image in jupyter/r-notebook section.
- [jupyter/r-notebook](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-r-notebook)
