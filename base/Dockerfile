FROM ubuntu

ENV  SIFT_GPU_URL  http://wwwx.cs.unc.edu/~ccwu/cgi-bin/siftgpu.cgi
ENV  SIFT_GPU_SHA1 eac08305f14cb35d12a22d493f84f9c21f6b7fdb
ENV  PBA_URL       http://grail.cs.washington.edu/projects/mcba/pba_v1.0.5.zip
ENV  PBA_SHA1      4d8d4d1a82f886b64bf7b94af2be17f14738e542

ENV  RUNTIME_DEPS  libglew1.13 libdevil1c2 freeglut3
ENV  BUILD_DEPS    curl unzip make cmake gcc g++ libgl1-mesa-dev \
                   freeglut3-dev libglew-dev libxi-dev libxmu-dev libdevil-dev

WORKDIR /usr/src

RUN apt-get -qy update && apt-get -qy install $RUNTIME_DEPS $BUILD_DEPS \
    ## SiftGPU \
    && curl -L -o /tmp/sift_gpu.zip $SIFT_GPU_URL \
    && echo "$SIFT_GPU_SHA1  /tmp/sift_gpu.zip" | sha1sum -c \
    && unzip /tmp/sift_gpu.zip && rm /tmp/sift_gpu.zip \
    && cd SiftGPU \
    && rm -rf bin/* && make \
    && mv bin/*.so bin/*.a /usr/local/lib/ \
    && mv bin/*            /usr/local/bin/ \
    && cd .. \
    ## PBA \
    && curl -L -o /tmp/pba.zip $PBA_URL \
    && echo "$PBA_SHA1  /tmp/pba.zip" | sha1sum -c \
    && unzip /tmp/pba.zip && rm /tmp/pba.zip \
    && cd pba && rm -rf bin/* && make -f makefile_no_gpu \
    && mv bin/*.so bin/*.a /usr/local/lib \
    && cd .. \
    ## CMVS-PMMVS \
    && mkdir -p /usr/src/cmvs-pmvs/build \
    && curl -L https://github.com/pmoulon/CMVS-PMVS/archive/master.tar.gz \
    | tar -C /usr/src/cmvs-pmvs --strip-components 2 -xzf - CMVS-PMVS-master/program \
    && cd cmvs-pmvs/build && cmake .. \
    && make install && mv main/cmvs main/genOption main/pmvs2 /usr/local/bin \
    && apt-get purge -qy --auto-remove $BUILD_DEPS \
    && rm -rf /usr/src/*
