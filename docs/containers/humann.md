---
sort: 1
---
# Humann 3

This is the definition file for humann3, at the moment not available from
Bioconda:


```text
Bootstrap: docker
From: centos:centos7.6.1810


%environment
    source /opt/software/conda/bin/activate /opt/software/conda_env


%post
    yum -y install epel-release wget which nano curl zlib-devel
    yum -y groupinstall "Development Tools"

    mkdir -p /opt/software

    cd /opt/software
    curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sh ./Miniconda3-latest-Linux-x86_64.sh -p /opt/software/conda -b

    /opt/software/conda/bin/conda config --add channels defaults
    /opt/software/conda/bin/conda config --add channels conda-forge
    /opt/software/conda/bin/conda config --add channels bioconda
    /opt/software/conda/bin/conda config --add channels biobakery
    /opt/software/conda/bin/conda create -p /opt/software/conda_env -y humann    
    source /opt/software/conda/bin/activate /opt/software/conda_env

    cd /opt/software

%runscript
    exec humann "$@"
```