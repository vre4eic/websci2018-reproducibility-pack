# websci2018-reproducibility-pack
Repo with materials to reproduce all data analysis, figures and tables of our Web Science 2018 paper: 
> Hollink, Laura, Astrid van Aggelen, and Jacco van Ossenbruggen. 
> [Using the Web of Data to Study Gender Differences in Online Knowledge Sources: the Case of the European Parliament](https://ir.cwi.nl/pub/27616) 
> ACM Conference on Web Science. May 2018, Amsterdam, The Netherlands. doi:10.1145/3201064.3201108


# Online version
The simplest way to rerun the code is to ignore this repo and just point your browser to http://vre4eic.project.cwi.nl/gender/

This public swish web server contains all code in an executable notebook style interface.

# Docker version
This repo contains the materials to rebuild our public swish web server running at http://vre4eic.project.cwi.nl/gender/ 

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
