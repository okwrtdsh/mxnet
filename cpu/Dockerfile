FROM mxnet/python:latest

ENV LANG=C.UTF-8 \
	LC_ALL=C.UTF-8

RUN apt-get update -qq \
 && apt-get install --no-install-recommends -y \
	wget bzip2 ca-certificates \
	libglib2.0-0 libxext6 libsm6 libxrender1 \
	git mercurial subversion \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
 && wget --quiet https://repo.continuum.io/archive/Anaconda3-5.2.0-Linux-x86_64.sh -O ~/anaconda.sh \
 && /bin/bash ~/anaconda.sh -b -p /opt/conda \
 && rm ~/anaconda.sh

RUN apt-get update -qq \
 && apt-get install --no-install-recommends -y \
	curl grep sed dpkg \
	libgtk2.0-0 \
	graphviz \
 && TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` \
 && curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb \
 && dpkg -i tini.deb \
 && rm tini.deb \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

ENV PATH=/opt/conda/bin:$PATH \
	NOTEBOOK_DIR=/src/notebooks \
	NOTEBOOK_IP=0.0.0.0 \
	NOTEBOOK_PORT=8888

RUN conda install -y --quiet \
	jupyter \
	Pillow \
 && conda config --add channels conda-forge \
 && conda install -c https://conda.anaconda.org/menpo opencv3 \
 && pip3 --no-cache-dir install \
	pydot_ng \
	graphviz

ENTRYPOINT ["tini", "--"]
CMD jupyter notebook \
	--notebook-dir=${NOTEBOOK_DIR} \
	--ip=${NOTEBOOK_IP} \
	--port=${NOTEBOOK_PORT} \
	--NotebookApp.token='' \
	--no-browser \
	--allow-root
