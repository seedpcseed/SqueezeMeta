Bootstrap: docker
From: continuumio/miniconda3

%labels
    Author Patrick Seed
    Version v0.0.1

%help
   A container adopted from Tamames, J., & Puente-Sánchez, F. (2018). SqueezeMeta, A Highly Portable, 
   Fully Automatic Metagenomic Analysis Pipeline. Frontiers in Microbiology, 9, 3349.
  
%environment
    RELEASE_DATE=2020.02.13 
    LC_ALL=en_US.UTF-8 
    LANG=en_US.UTF-8
    PATH=$PATH:/opt/conda/bin:/opt/conda/SqueezeMeta:/opt/conda/SqueezeMeta/scripts:/opt/conda/SqueezeMeta/data

%files
   DATA_CONFIG /data/DATA_CONFIG

%post
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install -y wget git

    . /opt/conda/etc/profile.d/conda.sh
    conda install python=3.6
    conda install -c bioconda -c conda-forge -c fpusan squeezemeta

    rm -r /opt/conda/SqueezeMeta
 
    git clone http://github.com/seedpcseed/SqueezeMeta /opt/conda/SqueezeMeta

    wget -c http://silvani.cnb.csic.es/SqueezeMeta/classifier.tar.gz
    wget -c http://silvani.cnb.csic.es/SqueezeMeta/classifier.md5

    mv classifier.md5 /opt/conda/SqueezeMeta/lib/classifier.md5

    tar -xvf classifier.tar.gz -C /opt/conda/SqueezeMeta/lib
    rm classifier.tar.gz


    cd /opt/conda/SqueezeMeta/bin
    ln -s /opt/conda/SqueezeMeta/lib/classifier/classifier.jar . > /dev/null 2>&1

    mv /data/DATA_CONFIG /opt/conda/SqueezeMeta/lib/checkm/DATA_CONFIG

%runscript
    exec "$@"
