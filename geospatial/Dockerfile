FROM cyversevice/jupyterlab-tensorflow:2.2.9

USER root

RUN apt-get update && \
    apt-get install -y libfreetype6-dev pkg-config libx11-dev && \
    apt-get clean && \
    rm -rv /var/lib/apt/lists/*

RUN chown -R jovyan:jovyan /opt/conda
USER jovyan

RUN conda update -n base conda 

RUN conda config --remove channels defaults && \
    conda config --add channels conda-forge

RUN conda install --yes -c conda-forge \
    altair \
    awscli \
    bottleneck \
    contextily \
    cython \  
    dask \
    h5py \
    humanize \
    gcsfs \ 
    google-api-python-client \
    ipyparallel \
    ipyvolume \
    ipywidgets \
    matplotlib \
    ncurses \
    netcdf4 \
    nodejs \
    numcodecs \ 
    oauth2client \
    opencv \
    palettable \
    pandas \
    pathlib2 \
    pycrypto \
    pyhdf \
    pyresample \
    pyproj \
    pysal \
    rasterio \
    s3fs \
    scikit-learn \
    scikit-image \
    scipy \
    scikit-image \
    seaborn \
    shapely \
    six \
    spectral \
    statsmodels \
    tqdm \
    udunits2 \
    wget 

# Geospatial Conda Packages
RUN conda install --yes -c conda-forge \
    basemap \
    cartopy \
    earthengine-api \
    earthpy \
    entwine \
    fiona \    
    folium \     
    geemap \
    geopandas \
    ipyleaflet \
    pdal \
    planet \
    regionmask \
    satpy \
    xarray \
    xarray-topo \
    xarray-simlab \
    vega_datasets \
    zarr 

# add Tensorflow Probability -- late in the build may move to prior container sooner than later
RUN conda install -c conda-forge tensorflow-probability

RUN conda clean --all -f -y 

RUN jupyter labextension install \
    @bokeh/jupyter_bokeh \
    @jupyter-widgets/jupyterlab-manager \
    @jupyter-widgets/jupyterlab-sidecar \
    @jupyterlab/geojson-extension \
    @jupyterlab/toc \
    ipyvolume \
    itkwidgets \    
    jupyterlab_iframe \ 
    jupyter-leaflet \
    jupyter-threejs \
 && npm cache clean --force

# add bqplot extension
RUN jupyter labextension install bqplot && \
    jupyter nbextension install bqplot --py --symlink --sys-prefix && \ 
    jupyter nbextension enable --py --sys-prefix bqplot

RUN jupyter lab build

# pip install
RUN pip install xshape porder

RUN conda clean --all -f -y

USER root
# purge older nodejs
RUN apt purge nodejs -y

USER jovyan
WORKDIR /home/jovyan

# install iRODS plugin
RUN conda install -c conda-forge nodejs -y
RUN pip install jupyterlab_irods

USER root
RUN jupyter serverextension enable --py jupyterlab_irods
RUN jupyter labextension install ijab

USER jovyan

