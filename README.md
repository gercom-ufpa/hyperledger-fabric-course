# Instalação da Rede

## Pré-requisitos
```
sudo chmod +x preinstall.sh
./preinstall.sh
```

## Gerar os arquivos criptográficos da rede
```
cd artifacts/channel/
./create-artifacts.sh
```

## Subir os containers da rede Fabric Test
```
docker-compose up -d
```

## Criar o canal mychannel na rede
```
./createChannel.sh
```

## Instalação do Chaincode
```
./deployChaincode.sh
```


## Interação com Chaincode
```
./interact.sh
```

## Subir API
```
cd api/
./pre_API.sh
nodemon start
```
## Interagir com a API via POSTMAN e cURL
```
* Criar usuário para interagir com a rede

curl -X POST http://localhost:4000/users   -H "Content-Type: application/json"   -d '{
        "username": "Jeffson",
        "orgName": "Org1"

      }' | jq

* Interação 

curl -X POST http://localhost:4000/channels/mychannel/chaincodes/fabcar \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzI5NTI5MzAsInVzZXJuYW1lIjoiSmVmZnNvbiIsIm9yZ05hbWUiOiJPcmcxIiwiaWF0IjoxNzMyOTE2OTMwfQ.1zAx7wuljY7qmGn3KPTKG3JwFDV6SNWeNtY3QT7Djrk" \
-d '{
    "fcn": "createCar",
    "peers": ["peer0.org1.example.com","peer0.org2.example.com"],
    "ChaincodeName": "fabcar",
    "args": ["CAR556","SUBARU","IMPREZA","RED","Marco"]
  }' | jq

```

# Possíveis erros
Arquivo do pre-install não coloca no bashrc as variaveis do PATH 
```
echo '# Hyperledger Fabric binaries' >> ~/.bashrc
echo 'export PATH=/fabric-samples/bin:$PATH' >> ~/.bashrc
echo '# Nodejs' >> ~/.bashrc
echo 'VERSION=v12.19.0' >> ~/.bashrc
echo 'DISTRO=linux-x64' >> ~/.bashrc
echo 'export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH' >> ~/.bashrc

echo '# Go' >> ~/.bashrc
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```





