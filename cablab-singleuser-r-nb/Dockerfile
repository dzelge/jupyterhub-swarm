From quay.io/esdc/singleuser-julia-nb:0.5.2
LABEL maintainer="Brockmann Consult GmbH <http://www.brockmann-consult.de>"

# Install R and R CABLAB
USER root
WORKDIR /srv/jupyterhub
RUN echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 
RUN apt-get -y update
RUN apt-get -y upgrade
# install R based on the instruction here https://askubuntu.com/questions/1032842/r-rstudio-installation-script-for-ubuntu-18-04-tdd-packages
RUN apt-get -y install gdebi libssl-dev libcurl4-openssl-dev libopenblas-dev libxml2-dev libxslt-dev r-base r-base-dev

RUN git clone https://github.com/esa-esdl/RCABLAB
RUN wget https://cran.r-project.org/src/contrib/Archive/RNetCDF/RNetCDF_1.6.1-2.tar.gz
RUN R CMD INSTALL RNetCDF_1.6.1-2.tar.gz
WORKDIR /srv/jupyterhub/RCABLAB
RUN git checkout 02998cd41ee0c3862cf698b6729471576366dd67
RUN R CMD INSTALL RCABLAB
WORKDIR /srv/jupyterhub
RUN apt-get -y install libcurl4-openssl-dev libssl-dev
RUN R -e "install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'),repos='http://cran.us.r-project.org');devtools::install_github('IRkernel/IRkernel');IRkernel::installspec()"
RUN R -e "install.packages(c('data.table'),repos='http://cran.us.r-project.org')"
RUN R -e "install.packages(c('ggplot2','raster','sp','zoo','rgdal','dplyr','vegan','ape','Rtsne','Rcpp','inline'),repos='http://cran.us.r-project.org')"

USER $NB_USER
WORKDIR /home/jovyan/work
