# websci2018-reproducibility-pack
Repo with materials to reproduce all data analysis, figures and tables of the Web Science 2018 paper: Using the Web of Data to Study Gender Differences in Online Knowledge Sources: the Case of the European Parliament [link to paper will be added asap]

# Online version
The simplest way to rerun the code is to ignore this repo and just point your browser to http://media.cwi.nl/gender/
This public swish web server contains all code in an executable notebook style interface.

# Docker version
This repo contains the materials to rebuild our public swish web server that is also running at http://media.cwi.nl/gender/
Our server is started by running 
```bash
docker-compose up -d
``` 
on the docker-compose.yml file contained in this repo. 

Provided that you have docker and docker-compose set up on your machine, just running the above command should pull the docker images from docker hub and start the webserver at localhost:3052.

# Virtual machine image version
[link to vm image to be added]

# Soure code version
The repo also used git submodules to link to other git repositories with all source code used, run
```bash
git submodule update --init --recursive
```
to populated all source code submodules. This also include the repos to rebuild the docker images used in the docker version.
