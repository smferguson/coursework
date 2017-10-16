FROM continuumio/anaconda:4.2.0
MAINTAINER Paulo Castro

# build: docker build -t coursera/ml-foundations .
# You can get your licence from https://turi.com/download/install-graphlab-create.html
# Free for student using coursera
ENV graphLabLicense "<INSERT KEY HERE>"

RUN conda create --yes -n gl-env python=2.7 anaconda=4.0.0

# Workaround to source command work!
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN source /opt/conda/bin/activate gl-env
RUN conda update --yes pip
RUN source /opt/conda/bin/activate gl-env && pip install --upgrade --no-cache-dir https://get.graphlab.com/GraphLab-Create/2.1/${graphLabLicense}/GraphLab-Create-License.tar.gz
RUN conda install --yes ipython-notebook
# Jupyter working like server inside docker machine
RUN source /opt/conda/bin/activate gl-env; jupyter notebook --generate-config; echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py

RUN apt-get install libgomp1

EXPOSE 8888

# Starting jupyter web interface
CMD source /opt/conda/bin/activate gl-env; ipython notebook -y --no-browser
