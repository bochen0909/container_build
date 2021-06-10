# docker build -t lizhen0909/binning .
FROM centos:centos8

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN yum update  -y && yum install -y python38.x86_64 python38-devel.x86_64 python3-pip cmake make gcc-c++  wget git boost-devel zlib-devel unzip && \
    alternatives --set python3 /usr/bin/python3.8 && \
    alternatives --set python /usr/bin/python3.8 && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    pwd

RUN pip3 --no-cache-dir install numpy matplotlib pysam checkm-genome

##concoct cocacola
RUN  wget https://github.com/BinPro/CONCOCT/archive/refs/tags/1.1.0.tar.gz  && \
    tar -xzf 1.1.0.tar.gz && \
    cd CONCOCT-1.1.0 && \
    make && \
    python setup.py install && \
    cp -r scripts/* /usr/local/bin 

    ##metabat
RUN wget https://bitbucket.org/berkeleylab/metabat/downloads/metabat-static-binary-linux-x64_v2.12.1.tar.gz && \
    tar -xzf metabat-static-binary-linux-x64_v2.12.1.tar.gz && \
    rm metabat-static-binary-linux-x64_v2.12.1.tar.gz && \
    chmod +x metabat/* && \
    mv metabat/* /usr/local/bin 

    ##canopy
RUN  git clone https://bitbucket.org/HeyHo/mgs-canopy-algorithm.git  && \
    cd mgs-canopy-algorithm  && \
    mkdir build && cd build && cmake .. && make -f Makefile && \
    ls -alrt && \
    mv canopy  /usr/local/bin 

RUN  wget http://eddylab.org/software/hmmer/hmmer-3.3.2.tar.gz && \
     tar xf hmmer-3.3.2.tar.gz && \
     cd hmmer-3.3.2 && \
     ./configure  && make && make install

RUN wget https://github.com/hyattpd/Prodigal/archive/refs/tags/v2.6.3.tar.gz && \
    tar xf v2.6.3.tar.gz && \
    cd Prodigal-2.6.3 && make && make install

RUN wget https://github.com/matsen/pplacer/releases/download/v1.1.alpha19/pplacer-linux-v1.1.alpha19.zip && \
    unzip pplacer*.zip  && \ 
    cp -r  pplacer-Linux-v1.1.alpha19/* /usr/local/bin/

RUN ls -alrt /usr/local/bin/   && ls  / && python3 --version

CMD [ "/bin/bash" ]


