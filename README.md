# install-reco-in-docker

This is a tutorial to teach how to install RECO in docker with dockerfiles. (ubuntu 14.04)

## Installing

### Build docker images

cd install-reco-in-docker/hss/ </br>
docker build -t "reco_hss" . </br>

cd install-reco-in-docker/mme/ </br>
docker build -t "reco_mme" . </br>

cd install-reco-in-docker/spgw/ </br>
docker build -t "reco_spgw" . </br>

### Create docker network

docker network create --driver=bridge --subnet=172.18.0.0/24 --gateway=172.18.0.1 reco_net

### Run RECO

docker run --ip=172.18.0.2 --net=reco_net -it reco_hss (must run hss before mme) </br>
docker run --ip=172.18.0.3 --net=reco_net -h ubuntu -ti reco_mme </br>
docker run --privileged=true -it -v /lib/modules:/lib/modules --ip=172.18.0.4 --net=reco_net reco_spgw </br>

