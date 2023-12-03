##################################

#

# SECTION SETUP

#

##################################

# move to the mount folder

cd ~

# download the package

curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.2.0 1.4.7

# move to the samples that we downloaded

cd ~/fabric-samples

# copy the binaries to our usr/localbin directory

sudo cp ./bin/\* /usr/local

# move to mount

cd mount

# create our base folder structure

mkdir network
mkdir chaincode
mkdir config

# move to samples folder

cd ~/fabric-samples

# copy the components that we need to our folder structure

cp -r test-network/_ ../mount/network
cp -r config/_ ../mount/config
cp -r chaincode/\* ../mount/chaincode

# test our basic setup

cd ~/mount/network
./network.sh up

# to bring down the network

./network.sh down
