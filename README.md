# Install Fabric
1. For new Droplets, always set the locale (choose en_US.UTF-8 if in doubt) and do apt update/upgrade.对于新的Droplet，请始终选择进行区域设置（如有疑问，请选择en_US.UTF-8）然后运行apt update/upgrade执行更新/升级。
```
sudo dpkg-reconfigure locales
sudo apt-get update && sudo apt-get upgrade
```
2. Setup a new user, it’s good practice not to use root to install these.创建新用户，建议不使用根用户安装
```
sudo adduser frog
sudo usermod -aG sudo frog
#切换用户
su - frog
```
3. Set up the Prerequisites, logout and log back in as frog.安装运行Hyperledger所需的组件，然后登出新用户再登入。
```
#下载Hyperledger Fabric依赖环境。
curl -O https://raw.githubusercontent.com/yangshanxiu007/two-org/main/prereqs-ubuntu.sh
chmod u+x prereqs-ubuntu.sh
./prereqs-ubuntu.sh
#安装golang
wget https://dl.google.com/go/go1.14.13.linux-amd64.tar.gz
tar -xzvf go1.14.13.linux-amd64.tar.gz
sudo mv go/ /usr/local
#在文件.bashrc中编辑gopath
pico ~/.bashrc
#(添加以下两行到文件.bashrc)
export GOPATH=/usr/local/go
export PATH=$PATH:$GOPATH/bin
#退出当前用户再登录frog
exit
su - frog
```
4. 通过这一步骤你可以设置好超级账本Fabric v2.3所需的所有镜像。
```
curl -sSL https://bit.ly/2ysbOFE | bash -s 2.3.0
```

# 使用docker swarm 调度方式设置覆盖网络。
1. (节点 1) 请确保使用正确的节点1主机的IP地址。
```
docker swarm init --advertise-addr [Fabric-Node-IP]
```
2. 在节点2上运行以下命令
```
docker swarm join --token SWMTKN-1-52d9at8jqihc1k0kotf6ma4r70cjz9j1heyql9kas80fp1vmxc-2ll0unuehvj7q5ds6qsmpxk5a [Fabric-Node-IP]:2377
```
3. (节点 1) 通过以下命令就可以创建覆盖网络。
```
docker network create --attachable --driver overlay first-network
```
4. (节点 2) 使用以下命令创建一个busybox用于查看覆盖网络。
```
docker run -itd --name mybusybox --network first-network busybox
```

# new-two-org-ca
1. 下载 new-two-org-ca
```
git clone https://github.com/yangshanxiu007/new-two-org-ca.git
```
2. (节点 1) 生成通道凭证和证书,在共识节点创建通道区块。
```
cd fabric-samples
export PATH=$PATH:$PWD/bin
cd ../new-two-org-ca

sudo ./network.sh up -ca
sudo ./network.sh createChannel
```
3. (节点1) 压缩该文件然后上传到其他两个节点。你可以使用Filezilla。
```
sudo chmod -R 775 new-two-org-ca/
cd ..
tar -czvf new-two-org-ca.tar.gz new-two-org-ca
```
4. (节点2) 在各节点解压缩该文件。
```
tar -xzvf new-two-org-ca.tar.gz new-two-org-ca
```
5. (节点2) new-two-org-ca目录下，运行以下命令，为不同的组件配置docker容器。
```
sudo ./node2.sh up
```
6. (节点1) 把所有peer节点加入通道。
```
sudo ./mychannelup.sh
```

# 编辑know_hosts
vi /etc/hosts
[Fabric-Node-IP] orderer.example.com
[Fabric-Node-IP] orderer1.example.com
[Fabric-Node-IP] peer0.org1.example.com
[Fabric-Node-IP] orderer2.example.com
[Fabric-Node-IP] peer0.org2.example.com

# 安装chaincode
1. 修改fabric-samples文件夹中样例chaincode，替换~/fabric-samples/chaincode/asset-transfer-basic/chaincode-go/chaincode/smartcontract.go
2. 打包chaincode
```
pushd ../fabric-samples/chaincode/asset-transfer-basic/chaincode-go
GO111MODULE=on go mod vendor
popd
docker exec cli peer lifecycle chaincode package basic.tar.gz --path github.com/chaincode/asset-transfer-basic/chaincode-go --label basic_1
```
3. (节点1) 安装chaincode到节点1
```
docker exec cli peer lifecycle chaincode install basic.tar.gz
```
4. (节点1) 安装chaincode到节点2
```
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode install basic.tar.gz
```
5. (节点1) org1 approve合约
```
docker exec cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name basic --version 1 --sequence 1 --waitForEvent --package-id basic_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179
```
6. (节点1) org2 approve合约
```
docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer lifecycle chaincode approveformyorg --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --channelID mychannel --name basic --version 1 --sequence 1 --waitForEvent --package-id basic_1:a976a3f2eb95c19b91322fc939dd37135837e0cfc5d52e4dbc3a2ef881d14179
```
7. (节点1) Commit chaincode
```
docker exec cli peer lifecycle chaincode commit -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt --channelID mychannel --name basic --version 1 --sequence 1

To check commit status,
docker exec cli peer lifecycle chaincode querycommitted --channelID mychannel --name basic
```
8. (节点1) 初始化
```
docker exec cli peer chaincode invoke -o orderer.example.com:7050 --tls true --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C mychannel -n basic --peerAddresses peer0.org1.example.com:7051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --peerAddresses peer0.org2.example.com:9051 --tlsRootCertFiles /opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c '{"Args":["InitLedger"]}'
```
9. (节点1) 查询
```
docker exec cli peer chaincode query -n basic -C mychannel -c '{"Args":["ReadAsset","0"]}'

docker exec -e CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp -e CORE_PEER_ADDRESS=peer0.org2.example.com:9051 -e CORE_PEER_LOCALMSPID="Org2MSP" -e CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt cli peer chaincode query -n basic -C mychannel -c '{"Args":["ReadAsset","0"]}'
```

# 安装apiserver
1. 安装依赖
```
sudo chmod -R 777 basic_apiserver
npm install
```
2. 测试功能
```
node enrollAdmin.js  注册admin
node registerUser.js 注册用户
node query.js  查询
node invoke.js 添加数据
```
3. 安装pm2,启动项目,查看运行端口
```
npm install -g pm2
pm2 start apiserver.js
netstat -ntlp | grep LISTEN
```

# 安装explorer
1. 下载 blockchain-explorer
```
git clone https://github.com/hyperledger/blockchain-explorer.git
```
2. 如有需要, Modify blockchain-explorer/app/explorerconfig.json to update PostgreSQL database settings.
```
"postgreSQL": {
    "host": "127.0.0.1",
    "port": "5432",
    "database": "fabricexplorer",
    "username": "hppoc",
    "passwd": "password"
}
```
3. 赋予数据库脚本权限
```
cd blockchain-explorer/app/persistence/fabric/postgreSQL
chmod -R 775 db/
```
4. 更新配置文件 blockchain-explorer/app/platform/fabric/config.json
```
{
    "network-configs": {
        "first-network": {
            "name": "firstnetwork",
            "profile": "./connection-profile/first-network.json",
            "enableAuthentication": false
        }
    },
    "license": "Apache-2.0"
}
```
5. 更新first-network.json 文件 blockchain-explorer/app/platform/fabric/connection-profile/first-network.json
```
"adminPrivateKey": {
				"path": "/home/frog/new-two-org-ca/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/e578c75e1e30bb2463233f3d01f1b72075e7d1493af9eda5f7b2958c7dc9dbaa_sk"
			}
```
6. 创建数据库
```
cd blockchain-explorer/app/persistence/fabric/postgreSQL/db
sudo -u postgres ./createdb.sh
查看
sudo -u postgres psql -c '\l'

                                List of databases
      Name      |  Owner   | Encoding | Collate |  Ctype  |   Access privileges
----------------+----------+----------+---------+---------+-----------------------
 fabricexplorer | hppoc    | UTF8     | C.UTF-8 | C.UTF-8 |
 postgres       | postgres | UTF8     | C.UTF-8 | C.UTF-8 |
 template0      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
                |          |          |         |         | postgres=CTc/postgres
 template1      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
                |          |          |         |         | postgres=CTc/postgres
(4 rows)
sudo -u postgres psql fabricexplorer -c '\d'
                   List of relations
 Schema |           Name            |   Type   | Owner
--------+---------------------------+----------+-------
 public | blocks                    | table    | hppoc
 public | blocks_id_seq             | sequence | hppoc
 public | chaincodes                | table    | hppoc
 public | chaincodes_id_seq         | sequence | hppoc
 public | channel                   | table    | hppoc
 public | channel_id_seq            | sequence | hppoc
 public | orderer                   | table    | hppoc
 public | orderer_id_seq            | sequence | hppoc
 public | peer                      | table    | hppoc
 public | peer_id_seq               | sequence | hppoc
 public | peer_ref_chaincode        | table    | hppoc
 public | peer_ref_chaincode_id_seq | sequence | hppoc
 public | peer_ref_channel          | table    | hppoc
 public | peer_ref_channel_id_seq   | sequence | hppoc
 public | transactions              | table    | hppoc
 public | transactions_id_seq       | sequence | hppoc
 public | write_lock                | table    | hppoc
 public | write_lock_write_lock_seq | sequence | hppoc
(18 rows)
```
7. 安装依赖
```
./main.sh install
To install, run tests, and build project
./main.sh clean
To clean the /node_modules, client/node_modules client/build, client/coverage, app/test/node_modules directories
```
8. 运行
```
npm start
It will have the backend and GUI service up
npm run app-stop
It will stop the node server
Note: If Hyperledger Fabric network is deployed on other machine, please define the following environment variable
DISCOVERY_AS_LOCALHOST=false npm start
```

## check and open port
netstat -ntlp | grep LISTEN
netstat -ntlp | grep 8080
sudo ufw allow 8080

# teardown fabric network
``` 
./network.sh down
docker volume ls
docker volume prune
./node2.sh down
docker volume ls
docker volume prune
```