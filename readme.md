<!-- installation  -->
./install-fabric.sh docker samples binary

./install-fabric.sh --fabric-version 2.5.0 binary


<!-- start network -->
./network.sh up createChannel -ca -c mychannel -s couchdb

./network.sh deployCC -ccn basic -ccp ../asset-transfer-basic/chaincode-typescript -ccl typescript

<!-- inside test network -->
export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=$PWD/../config/

<!-- test blockchain -->
peer chaincode query -C mychannel -n basic -c '{"Args":["GetAllAssets"]}'
peer chaincode query -C mychannel -n basic -c '{"Args":["ReadAsset","asset6"]}'

<!-- destroy network  -->
./network.sh down
./network.sh up

