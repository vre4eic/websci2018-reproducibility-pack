# websci2018-reproducibility-pack
This repository contains the materials to reproduce all figures, tables and other data analysis results reported in our Web Science 2018 paper: 

Hollink, Laura, Astrid van Aggelen, and Jacco van Ossenbruggen. 
[Using the Web of Data to Study Gender Differences in Online Knowledge Sources: the Case of the European Parliament](https://ir.cwi.nl/pub/27616). 
ACM Conference on Web Science, May 2018, Amsterdam, The Netherlands. 
[doi:10.1145/3201064.3201108](https://doi.org/10.1145/3201064.3201108)

A copy for long time archival of the repo has been uploaded to https://doi.org/10.5281/zenodo.1232929.

A [H2020 "FAIR" data management plan](data-management-plan.md) is included.

# Online version
The simplest way to rerun the code for the paper is to ignore this repo and just point your browser to https://vre4eic.project.cwi.nl/gender/p/tables_and_figures_from_paper.swinb

This public swish web server contains all code in an executable notebook style interface. We will try to keep this server up and running. In case it is down anyway, below are several options to rebuild the server yourself.

# Docker version
This repo contains the materials to start your own copy of the above server using docker. It is started by simply running 

```bash
docker-compose up -d
``` 
using the [docker-compose](docker-compose.yml) file contained in this repo. 

Provided that you have docker and docker-compose set up on your machine, just running the above command should pull the [images from docker hub](https://hub.docker.com/u/vre4eic/) and start the webserver at your own computer. To test, just point your web browser to http://localhost:3052/gender/p/tables_and_figures_from_paper.swinb

# Virtual machine image version
A virtual machine image is available from https://doi.org/10.5281/zenodo.1237673. It is archived as an Open Virtual Appliance (.ova file) that is packaging the vmdk disk image with an Open Virtual Machine Format (ovf) metadata descriptor. The image is based on a standard Ubuntu 17.04 iso image, with checked-out versions of all relevant source code and data (see below) and installed version of the docker images (see above).

On bootup, the docker images running in the guest will start a web server that is available from the host at 127.0.0.1:3052/gender/p/tables_and_figures_from_paper.swinb.

The virtual machine can be accessed using the user name "vre" with password "vrevre".

# Soure code version
The repo contains git submodules linking to other git repositories with source code of other projects used in the paper, run
```bash
git submodule update --init --recursive
```
to populated all source code submodules. 

The repos to rebuild the docker images used in the docker version are also included.

# Data used
The paper uses data from three RDF named graphs, stored in gzipped turtle file format. These files are included in the vre4eic/gender-demo-data docker image in the /data/toe directory and have the associated md5sum values: 
```
070ca73229931c9d0dd4cc1e4648ed75  Events_and_structure.ttl.gz
3ab7d22806fca083de6b4fd748392913  MembersOfParliament_background.ttl.gz
8717380919675bf732941f3aa03e3fcd  mep_wikidata.ttl.gz
```

These file are also in the gender-demo-data git submodule, as part of the ./gender-demo-data/toe.tgz gzipped tar file.

All three named graphs have been downloaded from the Talk of Europe project website, see http://www.talkofeurope.eu/ and http://linkedpolitics.ops.few.vu.nl/

If you use this data, please cite the corresponding open access paper:

Astrid van Aggelen, Laura Hollink, Max Kemman, Martijn Kleppe, Henri Beunders. The debates of the European Parliament as Linked Open Data. Semantic Web 8(2), pp. 271-281, 2017, IOS Press
https://doi.org/10.3233/SW-160227.

The mep\_wikidata graph has been generated by querying wikidata.org on all triples of which the object or subject is a resource with a MEP ID property (P1186).
The queries have been executed on 2018-04-03, and the following queries where used:
* https://query.wikidata.org/sparql?query=%0ASELECT%20?mep%20?mepLabel%20?mep_id%20?genderLabel%20WHERE%0A%7B%0A%20%20?mep%20wdt%3AP1186%20?mep_id%20.%0A%20%20OPTIONAL%20%7B%20?mep%20wdt%3AP21%20?gender%20.%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%7D%0A%7D%20ORDER%20BY%20?mep_id%0A#
* https://query.wikidata.org/sparql?query=CONSTRUCT%20%7B?subj%20?prop%20?mep.%7D%20WHERE%0A%7B%0A%20%20?mep%20wdt%3AP1186%20?mep_id%20.%0A%20%20?subj%20?prop%20?mep%20.%0A%7D%0A#
* https://query.wikidata.org/sparql?query=%0ACONSTRUCT%20%7B?mep%20?dprop%20?value.%20?dprop%20rdfs%3Alabel%20?propLabel%20%7D%20WHERE%0A%7B%0A%20%20?mep%20wdt%3AP1186%20?mep_id%20.%0A%20%20?mep%20?dprop%20?value%20.%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%20%20?prop%20wikibase%3AdirectClaim%20?dprop%20.%0A%20%20%20%20%20%20?prop%20rdfs%3Alabel%20?propLabel%20.%0A%20%20%20%20%20%20FILTER%20(lang(?propLabel)%20%3D%20%22en%22%20)%0A%20%20%7D%0A%7D%0A#

The MembersOfParliament\_background graph has been generated by a conversion to RDF of the CSV data obtained at 2018-04-09 from https://nabu.usit.uio.no/sv/isv/sendquery.php?query=%7B%22bool%22:%7B%22must%22:%5B%7B%22range%22:%7B%22parliament.to%22:%7B%22gte%22:%2219690720%22%7D%7D%7D,%7B%22range%22:%7B%22parliament.from%22:%7B%22lte%22:%2220180801%22%7D%7D%7D%5D%7D%7D

The Events\_and\_structure graph is the core graph of the Talk of Europe project and models in RDF all speeches in the European Parliament as crawled from http://europarl.europa.eu
More information on this data is available from the Talk of Europe data website http://linkedpolitics.ops.few.vu.nl/
