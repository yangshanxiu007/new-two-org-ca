## Running the test network

You can use the `./network.sh` script to stand up a simple Fabric test network. The test network has two peer organizations with one peer each and a single node raft ordering service. You can also use the `./network.sh` script to create channels and deploy chaincode. For more information, see [Using the Fabric test network](https://hyperledger-fabric.readthedocs.io/en/latest/test_network.html). The test network is being introduced in Fabric v2.0 as the long term replacement for the `first-network` sample.

Before you can deploy the test network, you need to follow the instructions to [Install the Samples, Binaries and Docker Images](https://hyperledger-fabric.readthedocs.io/en/latest/install.html) in the Hyperledger Fabric documentation.

organizations/ordererOrganizations  organizations/peerOrganizations
system-genesis-block/
channel-artifacts/

## 
./network.sh up 
./network.sh createChannel

network.sh

if [ ! -d "organizations/peerOrganizations" ]; then
    createOrgs
    createConsortium
  fi


  createChannel.sh
  ## Create channeltx
infoln "Generating channel create transaction '${CHANNEL_NAME}.tx'"
 createChannelTx

## Create anchorpeertx
infoln "Generating anchor peer update transactions"
 createAnchorPeerTx

FABRIC_CFG_PATH=$PWD/../config/

## Create channel
infoln "Creating channel ${CHANNEL_NAME}"
 createChannel


 crypto-config-orderer.yaml
  Specs:
      - Hostname: orderer
      - Hostname: orderer1
      - Hostname: orderer2

configtx.yaml
      OrdererType: etcdraft
            EtcdRaft:
                Consenters:
                - Host: orderer.example.com
                  Port: 7050
                  ClientTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer.example.com/tls/server.crt
                  ServerTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer.example.com/tls/server.crt
                - Host: orderer1.example.com
                  Port: 8050
                  ClientTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer1.example.com/tls/server.crt
                  ServerTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer1.example.com/tls/server.crt
                - Host: orderer2.example.com
                  Port: 9050
                  ClientTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer2.example.com/tls/server.crt
                  ServerTLSCert: ../organizations/ordererOrganizations/example.com/orderers/orderer2.example.com/tls/server.crt
            Addresses:
                - orderer.example.com:7050
                - orderer1.example.com:8050
                - orderer2.example.com:9050



## command  docker-compose-test-net_1.yaml
./node1.sh up 
./node1.sh createChannel

./node1.sh down
docker volume ls

docker volume prune

chmod -R 775 node1.sh 

createChannel.sh
## Join all the peers to the channel
infoln "Join Org1 peers to the channel..."
 joinChannel 1
infoln "Join Org2 peers to the channel..."
## joinChannel 2

## Set the anchor peers for each org in the channel
infoln "Updating anchor peers for org1..."
 updateAnchorPeers 1
infoln "Updating anchor peers for org2..."
## updateAnchorPeers 2


vi /etc/hosts
[Fabric-Node-IP] orderer.example.com
[Fabric-Node-IP] orderer1.example.com
[Fabric-Node-IP] peer0.org1.example.com
[Fabric-Node-IP] orderer2.example.com
[Fabric-Node-IP] peer0.org2.example.com

## add
[Fabric-Node-IP] ca.example.com
[Fabric-Node-IP] ca.org1.example.com
[Fabric-Node-IP] ca.org2.example.com

[Fabric-Node-IP] orderer0.example.com
[Fabric-Node-IP] peer0.org1.example.com
[Fabric-Node-IP] peer1.org1.example.com
[Fabric-Node-IP] peer2.org1.example.com



Step 5: 使用docker swarm 调度方式设置覆盖网络。
(节点 1) 请确保使用正确的节点1主机的IP地址。
docker swarm init --advertise-addr [Fabric-Node-IP]
在节点2和3上运行以下命令。
docker swarm join --token SWMTKN-1-52d9at8jqihc1k0kotf6ma4r70cjz9j1heyql9kas80fp1vmxc-2ll0unuehvj7q5ds6qsmpxk5a [Fabric-Node-IP]:2377
(节点 1) 通过以下命令就可以创建覆盖网络。
docker network create --attachable --driver overlay first-network
你可以使用命令docker network ls查看fabric swarm网络。 cldfd57gxqa4jg3u88gw0yda3
(节点 2 & 3) 使用以下命令创建一个busybox用于查看覆盖网络。
docker run -itd --name mybusybox --network first-network busybox

docker swarm 


sudo rm -rf docker-compose-test-net_1.yaml docker-compose-test-net_2.yaml



## command   docker-compose-test-net_2.yaml
./node2.sh up 
./node2.sh createChannel

./node2.sh down
docker volume ls

docker volume prune

chmod -R 775 node2.sh     

createChannel.sh
## Join all the peers to the channel
infoln "Join Org1 peers to the channel..."
 ## joinChannel 1
infoln "Join Org2 peers to the channel..."
   joinChannel 2

## Set the anchor peers for each org in the channel
infoln "Updating anchor peers for org1..."
 ## updateAnchorPeers 1
infoln "Updating anchor peers for org2..."
 	updateAnchorPeers 2


 ./network.sh down
docker volume prune

 sudo rm -rf docker-compose-test-net_1.yaml  docker-compose-test-net_2.yaml
sudo rm -rf channel-artifacts/

sudo rm -rf organizations/ordererOrganizations organizations/peerOrganizations
sudo rm -rf organizations/peerOrganizations

sudo chmod -R 775 docker/

sudo chmod -R 775 new-two-org/


sudo ./network.sh up
sudo ./network.sh createChannel

sudo ./node2.sh up
sudo ./node2.sh createChannel

sudo ./mychannelup.sh

docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer channel join -b mychannel.block


cli
volumes:
  - /var/run/:/host/var/run/
  - ../../chaincode/:/opt/gopath/src/github.com/chaincode
  - ../organizations:/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations
  - ../scripts:/opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/


Package chaincode
# If not done before
pushd ../chaincode/fabcar/go
GO111MODULE=on go mod vendor
popd
# packaging
docker exec cli peer lifecycle chaincode package fabcar.tar.gz --path github.com/chaincode/fabcar/go --label fabcar_1
Install chaincode package to all peers


# peer0.org1
docker exec cli peer lifecycle chaincode install fabcar.tar.gz

# peer0.org2
  docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode install fabcar.tar.gz

  docker images dev-*


  # for org1
docker exec cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name fabcar --version 1 --sequence 1 --waitForEvent --package-id fabcar_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179

2021-01-06 09:10:47.501 UTC [cli.lifecycle.chaincode] setOrdererClient -> INFO 001 Retrieved channel (mychannel) orderer endpoint: orderer.example.com:7050
2021-01-06 09:10:49.569 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [98342f4597a7da3ee70bef514127daf05ee727a38f512171b9276af41f122cad] committed with status (VALID) at peer0.org1.example.com:7051
# for org2
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name fabcar --version 1 --sequence 1 --waitForEvent --package-id fabcar_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179

2021-01-06 09:11:12.366 UTC [cli.lifecycle.chaincode] setOrdererClient -> INFO 001 Retrieved channel (mychannel) orderer endpoint: orderer.example.com:7050
2021-01-06 09:11:14.425 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [37cffa91e1615548c248b21b4462dfac9db79998d6d0e0cc44106d8baa6ed94f] committed with status (VALID) at peer0.org2.example.com:9051


docker exec cli peer lifecycle chaincode checkcommitreadiness --channelID mychannel --name fabcar --version 1 --sequence 1
Chaincode definition for chaincode 'fabcar', version '1', sequence '1' on channel 'mychannel' approval status by org:
Org1MSP: true
Org2MSP: true


## Commit chaincode
docker exec cli peer lifecycle chaincode commit -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt --channelID mychannel --name fabcar --version 1 --sequence 1

2021-01-06 09:12:54.695 UTC [chaincodeCmd] ClientWait -> INFO 001 txid [5fc7651c629ec5b767ce6a47b24116da1fb72a26590fcf20a11965eef99d0427] committed with status (VALID) at peer0.org1.example.com:7051
2021-01-06 09:12:54.904 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [5fc7651c629ec5b767ce6a47b24116da1fb72a26590fcf20a11965eef99d0427] committed with status (VALID) at peer0.org2.example.com:9051

To check commit status,
docker exec cli peer lifecycle chaincode querycommitted --channelID mychannel --name fabcar

docker exec cli peer lifecycle chaincode querycommitted --channelID mychannel --name fabcar
Committed chaincode definition for chaincode 'fabcar' on channel 'mychannel':
Version: 1, Sequence: 1, Endorsement Plugin: escc, Validation Plugin: vscc, Approvals: [Org1MSP: true, Org2MSP: true]


docker exec cli peer chaincode invoke -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n fabcar --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"Args":["initLedger"]}'


Query queryCar
After that, we can query a car record on the four peer nodes. We get back the same result. This shows that the fabric network is working well.
# peer0.org1
docker exec cli peer chaincode query -n fabcar -C mychannel -c '{"Args":["queryCar","CAR0"]}'


# peer0.org2
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer chaincode query -n fabcar -C mychannel -c '{"Args":["queryCar","CAR0"]}'


==========================

Package chaincode
# If not done before
pushd ../chaincode/asset-transfer-basic/chaincode-go

pushd ../asset-transfer-basic/chaincode-go
GO111MODULE=on go mod vendor
popd
# packaging
docker exec cli peer lifecycle chaincode package basic.tar.gz --path github.com/chaincode/asset-transfer-basic/chaincode-go --label basic_1
Install chaincode package to all peers


# peer0.org1
docker exec cli peer lifecycle chaincode install fabcar.tar.gz

# peer0.org2
  docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode install fabcar.tar.gz

  docker images dev-*


  # for org1
docker exec cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name fabcar --version 1 --sequence 1 --waitForEvent --package-id fabcar_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179

2021-01-06 09:10:47.501 UTC [cli.lifecycle.chaincode] setOrdererClient -> INFO 001 Retrieved channel (mychannel) orderer endpoint: orderer.example.com:7050
2021-01-06 09:10:49.569 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [98342f4597a7da3ee70bef514127daf05ee727a38f512171b9276af41f122cad] committed with status (VALID) at peer0.org1.example.com:7051
# for org2
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name fabcar --version 1 --sequence 1 --waitForEvent --package-id fabcar_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179

2021-01-06 09:11:12.366 UTC [cli.lifecycle.chaincode] setOrdererClient -> INFO 001 Retrieved channel (mychannel) orderer endpoint: orderer.example.com:7050
2021-01-06 09:11:14.425 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [37cffa91e1615548c248b21b4462dfac9db79998d6d0e0cc44106d8baa6ed94f] committed with status (VALID) at peer0.org2.example.com:9051


docker exec cli peer lifecycle chaincode checkcommitreadiness --channelID mychannel --name fabcar --version 1 --sequence 1
Chaincode definition for chaincode 'fabcar', version '1', sequence '1' on channel 'mychannel' approval status by org:
Org1MSP: true
Org2MSP: true


## Commit chaincode
docker exec cli peer lifecycle chaincode commit -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt --channelID mychannel --name fabcar --version 1 --sequence 1

2021-01-06 09:12:54.695 UTC [chaincodeCmd] ClientWait -> INFO 001 txid [5fc7651c629ec5b767ce6a47b24116da1fb72a26590fcf20a11965eef99d0427] committed with status (VALID) at peer0.org1.example.com:7051
2021-01-06 09:12:54.904 UTC [chaincodeCmd] ClientWait -> INFO 002 txid [5fc7651c629ec5b767ce6a47b24116da1fb72a26590fcf20a11965eef99d0427] committed with status (VALID) at peer0.org2.example.com:9051

To check commit status,
docker exec cli peer lifecycle chaincode querycommitted --channelID mychannel --name fabcar

docker exec cli peer lifecycle chaincode querycommitted --channelID mychannel --name fabcar
Committed chaincode definition for chaincode 'fabcar' on channel 'mychannel':
Version: 1, Sequence: 1, Endorsement Plugin: escc, Validation Plugin: vscc, Approvals: [Org1MSP: true, Org2MSP: true]


docker exec cli peer chaincode invoke -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n fabcar --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"Args":["initLedger"]}'


Query queryCar
After that, we can query a car record on the four peer nodes. We get back the same result. This shows that the fabric network is working well.
# peer0.org1
docker exec cli peer chaincode query -n fabcar -C mychannel -c '{"Args":["queryCar","CAR0"]}'


# peer0.org2
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer chaincode query -n fabcar -C mychannel -c '{"Args":["queryCar","CAR0"]}'


安装apiserver
sudo chmod -R 777 fabcar_apiserver
npm install

node enrollAdmin.js
node registerUser.js
node query.js
node invoke.js

安装pm2
npm install -g pm2

pm2 start apiserver.js

 netstat -ntlp | grep LISTEN



## auat1

CONTAINER ID   IMAGE                                                                                                                                                                   COMMAND                  CREATED       STATUS       PORTS                              NAMES
8f298234290d   dev-peer0.org1.example.com-fabcar_1-a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179-d9f4bbdb5d67f8c70702624aef58ffe6b0d4a96fd2dd61a1112f668f57d874ed   "chaincode -peer.add…"   2 hours ago   Up 2 hours                                      dev-peer0.org1.example.com-fabcar_1-a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179
adc39496fcd0   hyperledger/fabric-tools:latest                                                                                                                                         "/bin/bash"              3 hours ago   Up 3 hours                                      cli
e762e70a3dac   hyperledger/fabric-orderer:latest                                                                                                                                       "orderer"                3 hours ago   Up 3 hours   0.0.0.0:7050->7050/tcp             orderer.example.com
5667406ae6fc   hyperledger/fabric-orderer:latest                                                                                                                                       "orderer"                3 hours ago   Up 3 hours   7050/tcp, 0.0.0.0:8050->8050/tcp   orderer1.example.com
86e0ed2ef81a   hyperledger/fabric-peer:latest                                                                                                                                          "peer node start"        3 hours ago   Up 3 hours   0.0.0.0:7051->7051/tcp             peer0.org1.example.com




## auat2
CONTAINER ID   IMAGE                                                                                                                                                                   COMMAND                  CREATED       STATUS       PORTS                              NAMES
984c9ce35495   dev-peer0.org2.example.com-fabcar_1-a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179-4345bb056e1739702fd9169e9f9c6d165706b26123c29740763c464448dc3b8e   "chaincode -peer.add…"   2 hours ago   Up 2 hours                                      dev-peer0.org2.example.com-fabcar_1-a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179
fa51c7aaefbf   hyperledger/fabric-orderer:latest                                                                                                                                       "orderer"                3 hours ago   Up 3 hours   7050/tcp, 0.0.0.0:9050->9050/tcp   orderer2.example.com
b627937f1c4f   hyperledger/fabric-peer:latest                                                                                                                                          "peer node start"        3 hours ago   Up 3 hours   7051/tcp, 0.0.0.0:9051->9051/tcp   peer0.org2.example.com
16ecf92b5bba   busybox                                                                                                                                                                 "sh"                     7 hours ago   Up 7 hours                                      mybusybox




打开表
\c fabricexplorer
select * from peer;
select * from blocks;
postgres
sudo -u postgres psql
\l 显示所有数据库
\c fabricexplorer   进入某一个数据库
\dt 显示所有表
select * from chaincodes;
\q 退出

删除数据库 drop database fabricexplorer ;

删除chaincode
Peer 节点   
docker exec -ti 06c3d80bd71b bash
/var/hyperledger/production/chaincodes
===============================
~/blockchain-explorer/app/platform/fabric/connection-profile
first-network.json

./main.sh install
To install, run tests, and build project
./main.sh clean
To clean the /node_modules, client/node_modules client/build, client/coverage, app/test/node_modules directories
Or

$ cd blockchain-explorer
$ npm install
$ cd client/
$ npm install
$ npm run build

# Run Hyperledger Explorer
## Run Locally in Same Location
Modify app/explorerconfig.json to update sync settings.

"sync": {
  "type": "local"
}
npm start

It will have the backend and GUI service up
npm run app-stop

It will stop the node server
Note: If Hyperledger Fabric network is deployed on other machine, please define the following environment variable

$ DISCOVERY_AS_LOCALHOST=false npm start

## Run Standalone in Different Location
Modify app/explorerconfig.json to update sync settings.

"sync": {
  "type": "host"
}
If the Hyperledger Explorer was used previously in your browser be sure to clear the cache before relaunching

./syncstart.sh

It will have the sync node up
./syncstop.sh

It will stop the sync node
Note: If Hyperledger Fabric network is deployed on other machine, please define the following environment variable

$ DISCOVERY_AS_LOCALHOST=false ./syncstart.sh

## check and open port
netstat -ntlp | grep LISTEN
netstat -ntlp | grep 8080
sudo ufw allow 8080