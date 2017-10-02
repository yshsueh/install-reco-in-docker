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

docker network create --driver=bridge --subnet=192.188.2.0/24 --gateway=192.188.2.3 reco_net

### Run RECO

docker run --ip=192.188.2.4 --net=reco_net -it y51563118/reco_hss (must run hss before mme)
docker run --ip=192.188.2.2 --net=reco_net -h ubuntu -ti y51563118/reco_mme
docker run --privileged=true -it -v /lib/modules:/lib/modules --ip=192.188.2.5 --net=reco_net y51563118/reco_spgw

