FROM harbor.cyverse.org/vice/jupyter/tensorflow:latest

USER root

RUN apt-get update && \
    apt-get install -y libfreetype6-dev pkg-config libx11-dev && \
    apt-get clean && \
    rm -rv /var/lib/apt/lists/*

RUN apt purge nodejs -y

USER jovyan
WORKDIR /home/jovyan

COPY environment.yaml .

RUN conda config --add channels conda-forge
RUN conda update -n base conda 
RUN mamba env create -f environment.yaml

# Install JupyterLab Extensions
RUN pip install jupyterlab-geojson sidecar
RUN sudo chown -R 1000:100 /opt/conda/share
RUN jupyter labextension install \
    ipyvolume \
    itkwidgets \
    jupyterlab_iframe \
    jupyter-leaflet \
    jupyter-threejs \
    && npm cache clean --force

# add bqplot extension
RUN  conda install -c conda-forge bqplot && \
    jupyter nbextension install bqplot --py --symlink --sys-prefix && \ 
    jupyter nbextension enable bqplot --py --sys-prefix

RUN jupyter lab build

RUN conda clean --all -f -y

WORKDIR /home/jovyan