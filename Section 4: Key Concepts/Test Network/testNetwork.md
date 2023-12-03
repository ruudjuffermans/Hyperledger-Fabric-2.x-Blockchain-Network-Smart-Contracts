##################################
#                                #
#    TEST NETWORK                #
#                                #
##################################

##  connect the binaries
export PATH=/home/vagrant/mount/fabric-samples/bin:$PATH


# START THE NETWORK THE NETWORK #

## move to right directory
cd fabric-samples/test-network

## print helper function
./network.sh -h

## reset the network
./network.sh down

## start the network
./network.sh up

## show all the network nodes
docker ps -a


# CREATING A CHANNEL #

## create mychannel
./network.sh createChannel

## create channel2
./network.sh createChannel -c channel2

## shortcut
./network.sh up createChannel


# STARTING THE CHAINCODE #

## deploy chaincode
./network.sh deployCC


# INTERACTING WITH THE NETWORK

##  reach the binaries
export PATH=/home/vagrant/mount/fabric-samples/bin:$PATH

## configurations of the peer nodes
export FABRIC_CFG_PATH=$PWD/../config/

## set environment as ORG1
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org1MSP"
export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
export CORE_PEER_ADDRESS=localhost:7051

## initialize the ledger with assets
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n basic --peerAddresses localhost:7051 --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses localhost:9051 --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"function":"InitLedger","Args":[]}'


## query the ledger
peer chaincode query -C mychannel -n basic -c '{"Args":["GetAllAssets"]}'


## invoking the ledger
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile ${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n basic --peerAddresses localhost:7051 --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses localhost:9051 --tlsRootCertFiles ${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"function":"TransferAsset","Args":["asset6","Christopher"]}'

## set environment as ORG2
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org2MSP"
export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
export CORE_PEER_ADDRESS=localhost:9051

## query the ledger
peer chaincode query -C mychannel -n basic -c '{"Args":["ReadAsset","asset6"]}'

## bring down the network
./network.sh down
