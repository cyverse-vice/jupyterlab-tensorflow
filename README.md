[![Project Supported by CyVerse](https://img.shields.io/badge/Supported%20by-CyVerse-blue.svg)](https://learning.cyverse.org/projects/vice/en/latest/) [![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4543625.svg)](https://doi.org/10.5281/zenodo.4543625) [![license](https://img.shields.io/badge/license-BSD3-red.svg?style=flat-square)](https://opensource.org/licenses/BSD-3-Clause) ![GitHub all releases](https://img.shields.io/github/downloads/cyverse-vice/jupyterlab-tensorflow/total?style=flat-square)

# jupyterlab-tensorflow
[Project Jupyter](https://jupyter.org/) Tensorflow Notebook with CyVerse addins.

Jupyter Lab Tensorflow image built from the [Tensorflow Notebook](https://hub.docker.com/r/jupyter/tensorflow-notebook) for [CyVerse VICE](https://learning.cyverse.org/vice/about/). Project Jupyter's base image requires a couple additional configuration files for it be compatible with CyVerse Kubernetes orchestration and iRODS data store, which we have added.

CyVerse maintains a private [Harbor.io](https://goharbor.io) container registry. We push our containers from GitHub Actions to our Harbor, where they can be publicly re-used, or (re)built from GitHub pull requests. 

[![CircleCI](https://circleci.com/gh/cyverse-vice/jupyterlab-tensorflow.svg?style=svg)](https://circleci.com/gh/cyverse-vice/jupyterlab-tensorflow) [![Harbor](https://img.shields.io/badge/CyVerse%20Harbor-gray.svg?style=popout&logo=harbor)](https://harbor.cyverse.org/harbor/projects/17/repositories/jupyter%2Ftensorflow) ![GitHub commits since tagged version](https://img.shields.io/github/commits-since/cyverse-vice/jupyterlab-tensorflow/latest/main?style=flat-square) ![Action](https://github.com/cyverse-vice/jupyterlab-tensorflow/actions/workflows/harbor.yml/badge.svg)

quick launch | size | 
------------ | ---- | 
<a href="" target="_blank"><img src="https://img.shields.io/badge/Tensorflow-latest-orange?style=plastic&logo=tensorflow"></a> | [![SIZE](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-tensorflow/latest.svg)](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-tensorflow/latest) |
<a href="" target="_blank"><img src="https://img.shields.io/badge/Tensorflow-geospatial-orange?style=plastic&logo=tensorflow"></a> | [![SIZE](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-Tensorflow/geospatial.svg)](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-tensorflow/geospatial) |
<a href="https://de.cyverse.org/apps/de/07a2d5b2-76e2-11eb-be5f-008cfa5ae621/launch?quick-launch-id=60054c75-0e80-4169-8a9b-51cba04f756d" target="_blank"><img src="https://img.shields.io/badge/Tensorflow-2.2.9-orange?style=plastic&logo=tensorflow"></a> | [![SIZE](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-tensorflow/2.2.9.svg)](https://img.shields.io/docker/image-size/cyversevice/jupyterlab-tensorflow/2.2.9) |

# Instructions

## Run Docker locally or on a Virtual Machine

The container for running JupyterLab is hosted on DockerHub and can be started locally:

```
docker pull harbor.cyverse.org/vice/jupyter/tensorflow:latest
```

```
docker run -it --rm -d harbor.cyverse.org/vice/jupyter/tensorflow:latest
```

## Run Docker with NVIDIA GPU

```
docker run --gpus all -it --rm -d harbor.cyverse.org/vice/jupyter/tensorflow:latest
```

## Run Docker container in CyVerse VICE

Unless you plan on making changes to this container, you should just use the existing launch button above.

You can build a new Docker container with additional dependencies from this Docker Hub image by using the `FROM cyversevice/jupyterlab-tensorflow:latest` at the beginning of your own Dockerfile.

###### Developer notes

To test the container locally:

```
docker run --gpus all -it --rm -v /$HOME:/work --workdir /work -p 8888:8888 -e REDIRECT_URL=http://localhost:8888 harbor.cyverse.org/vice/jupyter/tensorflow:latest
```
