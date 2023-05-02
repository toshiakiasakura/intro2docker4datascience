FROM danhphan/pymc:4.0.0

RUN conda install -n pymc pymc==4.2.2
RUN /opt/conda/envs/pymc/bin/pip install jupyterlab # jupyterlab_vim
# !which -a pip

WORKDIR /home/jovyan/workspace
CMD ["conda", "run", "--no-capture-output", "-n", "pymc", "jupyter-lab","--ip=0.0.0.0","--port=8888","--no-browser","--allow-root"]
