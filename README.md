# 打卡系統上鏈用

## Hyperledger Composer 建置

1. 安裝NVM，可參考以下網址 [https://github.com/nvm-sh/nvm#install--update-script](https://github.com/nvm-sh/nvm#install--update-script)
2. 安裝node.js，建議用LTS版 or v8.1.1版
```
nvm install v8.1.1

or 

nvm install --lts
```

3. 安裝Docker，可參考以下網址 [https://docs.docker.com/install/linux/docker-ce/ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
4. 安裝Docker Composer 可參考以下網址 [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
5. 安裝Hyperledger Composer相關組件
```
npm install -g composer-cli
npm install -g composer-rest-server
npm install -g generator-hyperledger-composer
npm install -g yo
npm install -g composer-playground
```

6. 安裝Hyperledger Fabric Dev Server
```
curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
tar -xvf fabric-dev-servers.tar.gz
cd ~/fabric-dev-servers
./downloadFabric.sh
```

7. 啟動HYperledger環境
```
./startFabric.sh
```

8. 生成一張網路節點管理員卡
```
./createPeerAdminCard.sh
```

## Hyperledger Network 設定

1. 透過以下指令產生Hyperledger Network環境
```
composer archive create -t dir -n .
```

2. 將產生的網路環境設定卡安裝進Hyperledger
```
composer network install --card PeerAdmin@hlfv1 --archiveFile taipay-network@[版本號].bna
```

3. 產生網路管理員設置卡
```
composer network start --networkName taipay-network --networkVersion [網路環境設定卡版本號] --networkAdmin [網路管理員帳號] --networkAdminEnrollSecret [網路管理員密碼] --card PeerAdmin@hlfv1 --file networkadmin.card
```

4. 匯入網路管理員設置卡
```
composer card import --file networkadmin.card
```

5. 檢查Hyperledger Network是否設定成功
```
composer network ping --card [網路管理員帳號]@taipay-network
```

6. 生成REST API Server
```
composer-rest-server
```

## REST API Server 設定

1. 將[網路管理員帳號]@taipay-network做為匯入卡
2. 其他設定通通預設就好，預設它會用大寫顯示，好比(Y/n)