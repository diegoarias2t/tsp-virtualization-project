# Using official ubuntu image as a parent image
FROM ubuntu:18.04

# Setting the working directory to /project
WORKDIR /project

# Getting the updates for Ubuntu and installing openairinterface5g
RUN apt-get -y update && apt-get install -y git
RUN mkdir gitlab
RUN cd gitlab
RUN git clone https://gitlab.eurecom.fr/oai/openairinterface5g.git
RUN cd openairinterface5g
RUN git checkout develop
RUN source oaienv
RUN cd cmake_targets
RUN sudo ./build_oai -I
RUN sudo ./build_oai --gNB --nrUE
RUN cd ran_build/build
RUN make rfsimulator
RUN ln -s librfsimulator.so liboai_device.so
RUN sudo RFSIMULATOR=server ./nr-softmodem  ^`^sO ../../../targets/PROJECTS/GENERIC-LTE-EPC/CONF/gnb.band78.tm1.106PRB.usrpn300.conf  ^`^sparallel-config PARALLEL_SINGLE_THREAD --rfsim --phy-test