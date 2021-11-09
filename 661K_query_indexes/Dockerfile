# To build: docker build . -t leandroishilima/661k_query_indexes:0.0.1
# However, prefer to pull it from dockerhub: docker pull leandroishilima/661k_query_indexes:0.0.1
FROM continuumio/miniconda3

# configs
ARG cobs_repo_URL=https://github.com/bingmann/cobs/
ARG cobs_commit=05588df
ARG pp_sketchlib_version=1.5.1
ARG matplotlib_version=3.4.3
ARG pandas_version=1.3.4
ARG dendropy_version=4.5.2
ARG sourmash_version=3.5.0
ARG rapidnj_version=2.3.2


# install basic dependencies
RUN apt update && apt install -y cmake g++ git zlib1g-dev libboost-all-dev

# install cobs
RUN git clone --recursive $cobs_repo_URL && cd cobs && git checkout $cobs_commit && mkdir build && cd build && cmake .. && make -j4 && make test && cd /
# add cobs to path
ENV PATH="/cobs/build/src:${PATH}"

# install pp-sketchlib
RUN conda install -c conda-forge pp-sketchlib=$pp_sketchlib_version

# install python libs
RUN python -m pip install matplotlib==$matplotlib_version pandas==$pandas_version dendropy==$dendropy_version sourmash==$sourmash_version

# install rapidnj
RUN wget https://github.com/johnlees/rapidnj/archive/refs/tags/${rapidnj_version}.tar.gz -O rapidnj_${rapidnj_version}.tar.gz && tar -zxvf rapidnj_${rapidnj_version}.tar.gz && rm rapidnj_${rapidnj_version}.tar.gz && cd rapidnj-${rapidnj_version} && make -j4 && cd /
# add rapidnj to path
ENV PATH="/rapidnj-${rapidnj_version}/bin:${PATH}"
