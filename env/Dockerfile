FROM jupyter/base-notebook
USER root
RUN apt-get -y update 
RUN apt-get -y install golang
RUN apt-get -y install git
RUN apt-get -y install vim
USER $NB_UID 

RUN env GO111MODULE=on go get github.com/gopherdata/gophernotes
RUN mkdir -p /home/jovyan/.local/share/jupyter/kernels/gophernotes
WORKDIR /home/jovyan/.local/share/jupyter/kernels/gophernotes
RUN cp "$(go env GOPATH)"/pkg/mod/github.com/gopherdata/gophernotes@v0.7.1/kernel/*  "."
RUN sed "s|gophernotes|$(go env GOPATH)/bin/gophernotes|" < kernel.json.in > kernel.json.out 
RUN chmod +w kernel.json.out
RUN mv kernel.json.out kernel.json
#RUN chmod +w kernel.json

WORKDIR /home/jovyan/work/notebooks
COPY requirements.txt /opt/app/requirements.txt
RUN pip install -r /opt/app/requirements.txt

