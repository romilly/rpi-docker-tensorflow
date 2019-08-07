FROM arm32v7/python

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libhdf5-dev \
        libpng-dev \
        libzmq3-dev \
        pkg-config \
        python3-dev \
        python3-numpy \
        python3-scipy \
        rsync \
        unzip

RUN  apt-get clean && \
        rm -rf /var/lib/apt/lists/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
        rm get-pip.py

RUN pip --no-cache-dir install \
        matplotlib && \
        ipykernel \
        jupyter \
            python -m ipykernel.kernelspec

ADD tensorflow-1.14.0-cp37-cp37m-linux_armv7l.whl .

RUN pip install tensorflow-1.14.0-cp37-cp37m-linux_armv7l.whl

COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]
